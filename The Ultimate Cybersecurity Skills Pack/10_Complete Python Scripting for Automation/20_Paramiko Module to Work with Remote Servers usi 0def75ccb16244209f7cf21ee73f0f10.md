# 20_Paramiko Module to Work with Remote Servers using Python

## Paramiko Module(Used to work with remote servers):

- Paramiko module will create an SSH Client and by using this it will connect to a remote server and executes commands.
- we can also transfer files from the remote machine to the local one or vice versa using paramiko.
- Two ways to connect with the remote server:
    - Using username and password
    - Using a username and cryptographic key
- We connect to Linux/Windows <-> Linux/Windows

## An Example of Paramiko Scripting

```python
#!/bin/python
import paramiko

ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())

#Working with remote servers using username and password
ssh_client.connect(hostname='3.92.79.119', username='ec2-user', password='paramiko123', port=22)

stdin, stdout, stderr = ssh_client.exec_command('/bin/ls')
print("output:")
print(stdout.read())
print("error:")
print(stderr.read())

```

Here is a line-by-line explanation of the code:

- `#!/bin/python`: The script specifies that it is a Python script.
- `import paramiko`: This imports the Paramiko module.
- `ssh_client = paramiko.SSHClient()`: This creates an instance of the SSHClient class.
- `ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())`: This sets the policy for automatically adding the hostname and new host key to the local HostKeys object.
- `ssh_client.connect(hostname='3.92.79.119', username='ec2-user', password='paramiko123', port=22)`: This connects to the remote server using the specified hostname, username, password, and port.
- `stdin, stdout, stderr = ssh_client.exec_command('/bin/ls')`: This executes the specified command on the remote server.
- `print(stdout.read())`: This reads the output of the command and prints it out.
- `print(stderr.read())`: This reads the error, if any, and prints it out.

# Transfer File from Local Server to
Remote Server and Vice Versa using Paramiko

### Download

```python
import paramiko

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect(hostname='54.165.97.91', username='ec2-user', password='paramiko123', port=22)

sftp_client = ssh.open_sftp()
sftp_client.chdir('/home/ec2-user')
print(sftp_client.getcwd())
sftp_client.get('demo.txt', 'C:\\\\Users\\\\Automation\\\\Desktop\\\\download_file.txt')
sftp_client.close()
ssh.close()
```