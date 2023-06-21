# Chapter 3: Writing a Sniffer

# **Packet Sniffing on Windows and Linux**

## `sniffer.py`

```python
import socket
import os

# host to listen on
HOST = '127.0.0.1'

def main():
    # create raw socket, bind to public interface
    if os.name == 'nt': # checks if os is withndows
        socket_protocol = socket.IPPROTO_ICMP
    else:
        socket_protocol = socket.IPPROTO_IP

    # socket object with the parameters necessary for sniffing packets on our network interface
    sniffer = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket_protocol)
    sniffer.bind((HOST, 0))

    # include the IP header in the capture
    sniffer.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)

    if os.name == 'nt':
        sniffer.ioctl(socket.SIO_RCVALL, socket.RCVALL_ON)

    # read one packet
    print(sniffer.recvfrom(65565)) # printing out the entire raw packet

    if os.name == 'nt': # checks if os is withndows
        sniffer.ioctl(socket.SIO_RCVALL, socket.RCVALL_OFF) # disable promiscuous mode

if __name__ == '__main__':
    main()
```

The code above is a Python script that demonstrates how to capture and print out the contents of a single packet on a network interface. The script uses the `socket` module to create a raw socket and bind it to the public interface. It then sets the `IP_HDRINCL` option to include the IP header in the packet capture, reads one packet using `sniffer.recvfrom(65565)`, and prints out the entire raw packet in hexadecimal format. If the OS is Windows, the script enables promiscuous mode using `sniffer.ioctl()` and `RCVALL_ON` before reading the packet, and disables it using `sniffer.ioctl()` and `RCVALL_OFF` after reading the packet.

Here are more details on how the code works:

- The script imports the necessary modules, `socket` and `os`
- It sets the IP address of the host to listen to `127.0.0.1` (localhost)
- It checks the operating system and sets the `socket_protocol` to `socket.IPPROTO_ICMP` if the OS is Windows and `socket.IPPROTO_IP` if it's Linux.
- It creates a raw socket using `socket.socket()` with the parameters necessary for sniffing packets on the network interface.
- It binds the socket to the public interface using `sniffer.bind()`
- It sets the `IP_HDRINCL` option to include the IP header in the capture using `sniffer.setsockopt()`
- If the OS is Windows, it sets the `SIO_RCVALL` option to `RCVALL_ON` to enable promiscuous mode using `sniffer.ioctl()`.
- It reads one packet using `sniffer.recvfrom(65565)` and prints out the entire raw packet in hexadecimal format.
- If the OS is Windows, it disables promiscuous mode using `sniffer.ioctl()` and `RCVALL_OFF` after reading the packet.

## ***Kicking the Tires***

- This code is for **windows**

Run a fresh CMD in Administrator mode and run the code:

```powershell
python sniffer.py
```

Ping a website in another command promp:

```powershell
ping google.com
```

The output should be like this:

```powershell
(b'E\x00\x00T\xad\xcc\x00\x00\x80\x01\n\x17h\x14\xd1\x03\xac\x10\x9d\x9d\x00\x00g,\rv\x00\x01\xb6L\x1b^\x00\x00\x00\x00\xf1\xde\t\x00\x00\x00\x00\x00\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f!"#$%&\'()*+,-./01234567', ('104.20.209.3', 0))
```

# **Decoding the IP Layer**

![Screenshot 2023-06-19 at 11.03.25 AM.png](Chapter%203%20Writing%20a%20Sniffer%2096124a89ad834013a540ed3d4cb21121/Screenshot_2023-06-19_at_11.03.25_AM.png)

The image shows an example of an IP packet and its various fields.

- **Version:** The version of the IP protocol, which is usually 4 or 6.
- **Header Length:** The length of the IP header in 32-bit words. This field is important because it tells the receiver where the actual data starts in the packet.
- **Differentiated Services Code Point (DSCP):** A field that allows packets to be prioritized based on the type of traffic.
- **Explicit Congestion Notification (ECN):** A field that is used to avoid congestion in the network.
- **Total Length:** The total length of the IP packet, including the header and the data.
- **Identification:** A unique identifier for the IP packet.
- **Flags:** A set of three bits that are used to control fragmentation of the packet.
- **Fragment Offset:** The offset of the current fragment relative to the start of the original packet.
- **Time to Live (TTL):** A field that is used to limit the lifetime of the packet in the network.
- **Protocol:** The protocol used in the data portion of the packet.
- **Header Checksum:** A checksum of the IP header to ensure that the packet has not been corrupted in transit.
- **Source IP Address:** The IP address of the sender.
- **Destination IP Address:** The IP address of the receiver.

This information is important for understanding the structure of an IP packet and how it is used in communication over a network.

## **The `ctypes` Module**

The following code snippet defines a new class, IP, that can read a packet
and parse the header into its separate fields:

```python
from ctypes import *
import socket
import struct

class IP(Structure):
    _fields_ = [
        ("ihl", c_ubyte, 4), # 4 bit unsigned char
        ("version", c_ubyte, 4), # 4 bit unsigned char
        ("tos", c_ubyte, 8), # 1 byte char
        ("len", c_ushort, 16), # 2 byte unsigned short
        ("id", c_ushort, 16), # 2 byte unsigned short
        ("offset", c_ushort, 16), # 2 byte unsigned short
        ("ttl", c_ubyte, 8), # 1 byte char
        ("protocol_num", c_ubyte, 8), # 1 byte char
        ("sum", c_ushort, 16), # 2 byte unsigned short
        ("src", c_uint32, 32), # 4 byte unsigned int
        ("dst", c_uint32, 32) # 4 byte unsigned int
    ]

    def __new__(cls, socket_buffer=None):
        return cls.from_buffer_copy(socket_buffer)

    def __init__(self, socket_buffer=None):
        # human readable IP addresses
        self.src_address = socket.inet_ntoa(struct.pack("<L",self.src))
        self.dst_address = socket.inet_ntoa(struct.pack("<L",self.dst))
```

This code defines a `ctypes` Structure called `IP` that represents the various fields of an IP packet header. The `IP` structure is used to parse the packet data received by the sniffer in Chapter 3 of the document. The `_fields_` attribute defines the fields of the `IP` structure and their data types. The `__new__` method creates a new instance of the `IP` structure from the raw packet data received by the sniffer. The `__init__` method converts the `src` and `dst` fields of the `IP` structure from binary format to human-readable IP addresses using the `inet_ntoa` function from the `socket` module and the `pack` function from the `struct` module.

## **The struct Module**

The struct module provides format characters that you can use to specify the structure of the binary data. In the following example, we’ll once again define an IP class to hold the header information. This time, though, we’ll use format characters to represent the parts of the header:

```python
import ipaddress
import struct

class IP:
    def __init__(self, buff=None):
        header = struct.unpack('<BBHHHBBH4s4s', buff)
        self.ver = header[0] >> 4
        self.ihl = header[0] & 0xF
        self.tos = header[1]
        self.len = header[2]
        self.id = header[3]
        self.offset = header[4]
        self.ttl = header[5]
        self.protocol_num = header[6]
        self.sum = header[7]
        self.src = header[8]
        self.dst = header[9]
        # human readable IP addresses
        self.src_address = ipaddress.ip_address(self.src)
        self.dst_address = ipaddress.ip_address(self.dst)
        # map protocol constants to their names
        self.protocol_map = {1: "ICMP", 6: "TCP", 17: "UDP"}
```

The code above defines a class called `IP` that represents the various fields of an IP packet header. The `IP` class is used to parse the packet data received by the sniffer in Chapter 3 of the document. The `__init__` method takes in a byte buffer `buff` and uses the `struct.unpack` function to extract the various fields of the IP header. The IP addresses are then converted from binary format to human-readable IP addresses using the `ipaddress.ip_address` method. The `protocol_map` dictionary is used to map the protocol constants to their names.

In the `struct.unpack()` function in the `IP` class definition, `BBHHHBBH4s4s` is the format string that describes the structure of the IP header. Each character in the format string corresponds to a field in the header, and the number of characters indicates the size of each field in bytes. Here is what each character represents:

- `B`: unsigned char (1 byte)
- `H`: unsigned short (2 bytes)
- `4s`: 4-byte string
- `s`: string (1 byte)

So, `BBHHHBBH4s4s` corresponds to the following fields in the IP header:

- One byte for the version and header length fields `B`
- One byte for the type of service (TOS) field `B`
- Two bytes for the total length field `H`
- Two bytes for the identification field `H`
- Two bytes for the flags and fragment offset fields `H`
- One byte for the time to live (TTL) field `B`
- One byte for the protocol field `B`
- Two bytes for the header checksum field `H`
- Four bytes for the source IP address field `4s`
- Four bytes for the destination IP address field `4s`

![Screenshot 2023-06-19 at 11.03.25 AM.png](Chapter%203%20Writing%20a%20Sniffer%2096124a89ad834013a540ed3d4cb21121/Screenshot_2023-06-19_at_11.03.25_AM.png)

The fields are read in the order that they appear in the format string, and their values are returned in a tuple. The `unpack()` function takes the byte buffer as its argument and returns the tuple of field values.

The `IP` class can be used to parse the IP header of a packet as follows:

```python
ip_header = IP(packet[0:20])
print(f"Protocol: {ip_header.protocol_map[ip_header.protocol_num]}")
print(f"Source: {ip_header.src_address}")
print(f"Destination: {ip_header.dst_address}")
```

This code creates an instance of the `IP` class with the first 20 bytes of the packet, which contain the IP header. It then prints out the protocol, source IP address, and destination IP address of the packet.

# **Writing the IP Decoder**

Let’s implement the IP decoding routine. 

## *`sniffer_ip_header_decode.py`*

```python
import ipaddress
import os
import socket
import struct
import sys

class IP:
    def __init__(self, buff=None):

        # 'struct' module -> unpack binary data from a buffer -> based on a specified format.
        header = struct.unpack('<BBHHHBBH4s4s', buff) # format string '<BBHHHBBH4s4s' represents the structure of the IP header.

        self.ver = header[0] >> 4
        self.ihl = header[0] & 0xF
        self.tos = header[1]
        self.len = header[2]
        self.id = header[3]
        self.offset = header[4]
        self.ttl = header[5]
        self.protocol_num = header[6]
        self.sum = header[7]
        self.src = header[8]
        self.dst = header[9]

        # human readable IP addresses
        # 'ipaddress' module's function -> create an IPv4Address or IPv6Address object.
        self.src_address = ipaddress.ip_address(self.src) 
        self.dst_address = ipaddress.ip_address(self.dst)

        # map protocol constants to their names
        self.protocol_map = {1: "ICMP", 6: "TCP", 17: "UDP"}
        try:
            self.protocol = self.protocol_map[self.protocol_num]
        except Exception as e:
            print('%s No protocol for %s' % (e, self.protocol_num))
            self.protocol = str(self.protocol_num)

''''
    Previously explained & used on sniffer.py
'''
def sniff(host):
    # should look familiar from previous example
    if os.name == 'nt':
        socket_protocol = socket.IPPROTO_IP
    else:
        socket_protocol = socket.IPPROTO_ICMP
    sniffer = socket.socket(socket.AF_INET,
                            socket.SOCK_RAW, socket_protocol)
    sniffer.bind((host, 0))
    sniffer.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)
    if os.name == 'nt':
        sniffer.ioctl(socket.SIO_RCVALL, socket.RCVALL_ON)
    try:
        while True:
            # read a packet
            raw_buffer = sniffer.recvfrom(65535)[0]
            # create an IP header from the first 20 bytes
            ip_header = IP(raw_buffer[0:20])
            # print the detected protocol and hosts
            print('Protocol: %s %s -> %s' % (ip_header.protocol,
            ip_header.src_address,
            ip_header.dst_address))
    except KeyboardInterrupt:
        # if we're on Windows, turn off promiscuous mode
        if os.name == 'nt':
            sniffer.ioctl(socket.SIO_RCVALL, socket.RCVALL_OFF)
        sys.exit()

if __name__ == '__main__':
    if len(sys.argv) == 2:
        host = sys.argv[1]
    else:
        host = '192.168.1.203' # substitude with your machine's IPv4 address
    sniff(host)
```

The code above is a Python script that demonstrates how to sniff and print out the contents of a single IP packet on a network interface. The script uses the `socket` module to create a raw socket and bind it to the public interface. It then sets the `IP_HDRINCL` option to include the IP header in the packet capture, reads one packet using `sniffer.recvfrom(65535)[0]`, and prints out the protocol, source IP address, and destination IP address of the packet. If the OS is Windows, the script enables promiscuous mode using `sniffer.ioctl()` and `RCVALL_ON` before reading the packet, and disables it using `sniffer.ioctl()` and `RCVALL_OFF` after reading the packet.

### ***Kicking the Tires***

- Find your machine's IPv4 address in Windows using:
    
    ```powershell
    ipconfig 
    ```
    
    Substitute this ip with Host address. 
    

You can run the script in the command line by typing `python sniffer_ip_header_decode.py <host>`, where `<host>` is the IP address of the host you want to listen on. If no host is specified, the script will listen on the default host `192.168.1.203`.

# **Decoding ICMP**

![Screenshot 2023-06-19 at 1.19.09 PM.png](Chapter%203%20Writing%20a%20Sniffer%2096124a89ad834013a540ed3d4cb21121/Screenshot_2023-06-19_at_1.19.09_PM.png)

The picture above shows an example of an ICMP packet and its various fields. **ICMP** stands for **Internet Control Message Protocol**, and it is used to send error messages and operational information about network conditions. Here are the details of the fields in an ICMP packet:

- **Type:** The type of ICMP packet, which indicates the purpose of the message. Some common types of ICMP packets include Echo Request (Type 8), Echo Reply (Type 0), Destination Unreachable (Type 3), Time Exceeded (Type 11), and Redirect (Type 5).
- **Code:** A more specific identifier for the ICMP message. The meaning of the code depends on the type of message.
- **Checksum:** A checksum of the ICMP packet to ensure that it has not been corrupted in transit.
- **Identifier:** A unique identifier for the ICMP message, used to match requests and replies.
- **Sequence Number:** A sequence number for the ICMP message, used to match requests and replies.
- **Data:** Optional data that may be included in the message, such as the payload of an Echo Request or Reply.

This information is important for understanding the structure of an ICMP packet and how it is used in communication over a network.

## *`sniffer_with_icmp.py`*

```python
import ipaddress
import os
import socket
import struct
import sys

class IP:
    def __init__(self, buff=None):

        # 'struct' module -> unpack binary data from a buffer -> based on a specified format.
        header = struct.unpack('<BBHHHBBH4s4s', buff) # format string '<BBHHHBBH4s4s' represents the structure of the IP header.

        self.ver = header[0] >> 4
        self.ihl = header[0] & 0xF
        self.tos = header[1]
        self.len = header[2]
        self.id = header[3]
        self.offset = header[4]
        self.ttl = header[5]
        self.protocol_num = header[6]
        self.sum = header[7]
        self.src = header[8]
        self.dst = header[9]

        # human readable IP addresses
        # 'ipaddress' module's function -> create an IPv4Address or IPv6Address object.
        self.src_address = ipaddress.ip_address(self.src) 
        self.dst_address = ipaddress.ip_address(self.dst)

        # map protocol constants to their names
        self.protocol_map = {1: "ICMP", 6: "TCP", 17: "UDP"}
        try:
            self.protocol = self.protocol_map[self.protocol_num]
        except Exception as e:
            print('%s No protocol for %s' % (e, self.protocol_num))
            self.protocol = str(self.protocol_num)

class ICMP:
    def __init__(self, buff):
        header = struct.unpack('<BBHHH', buff)
        self.type = header[0]
        self.code = header[1]
        self.sum = header[2]
        self.id = header[3]
        self.seq = header[4]

def sniff(host):
    # should look familiar from previous example
    if os.name == 'nt':
        socket_protocol = socket.IPPROTO_IP
    else:
        socket_protocol = socket.IPPROTO_ICMP
    sniffer = socket.socket(socket.AF_INET,
                            socket.SOCK_RAW, socket_protocol)
    sniffer.bind((host, 0))
    sniffer.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)
    if os.name == 'nt':
        sniffer.ioctl(socket.SIO_RCVALL, socket.RCVALL_ON)
    try:
        while True:
            raw_buffer = sniffer.recvfrom(65535)[0]
            ip_header = IP(raw_buffer[0:20])
            # if it's ICMP, we want it
            if ip_header.protocol == "ICMP":
                print('Protocol: %s %s -> %s' % (ip_header.protocol,
                ip_header.src_address, 
                ip_header.dst_address))
                print(f'Version: {ip_header.ver}')
                print(f'Header Length: {ip_header.ihl} TTL: {ip_header.ttl}')

                # calculate where our ICMP packet starts
                offset = ip_header.ihl * 4
                buf = raw_buffer[offset:offset + 8]
                # create our ICMP structure
                icmp_header = ICMP(buf)
                print('ICMP -> Type: %s Code: %s\\n' %
                (icmp_header.type, 
                 icmp_header.code))
    except KeyboardInterrupt:
        if os.name == 'nt':
            sniffer.ioctl(socket.SIO_RCVALL, socket.RCVALL_OFF)
        sys.exit()

if __name__ == '__main__':
    if len(sys.argv) == 2:
        host = sys.argv[1]
    else:
        host = '192.168.1.203' # substitude with your machine's IPv4 address
    sniff(host)
```

This code is for sniffing ICMP packets and printing out relevant information, including the protocol, source IP address, destination IP address, version, header length, TTL, and ICMP type and code. The `IP` and `ICMP` classes are defined with the `_fields_` attribute specifying the fields of the IP and ICMP headers, respectively. The `__new__` method of each class creates a new instance of the class from the raw packet data received by the sniffer, and the `__init__` method initializes the instance attributes. The `sniff` function uses the `socket` module to create a raw socket and bind it to the public interface. It then sets the `IP_HDRINCL` option to include the IP header

## `Scanner.py`

```python
import ipaddress
import os
import socket
import struct
import sys
import threading
import time

# subnet to target
SUBNET = '192.168.1.0/24'
# magic string we'll check ICMP responses for
MESSAGE = 'PYTHONRULES!'

class IP:
    def __init__(self, buff=None):

        # 'struct' module -> unpack binary data from a buffer -> based on a specified format.
        header = struct.unpack('<BBHHHBBH4s4s', buff) # format string '<BBHHHBBH4s4s' represents the structure of the IP header.

        self.ver = header[0] >> 4
        self.ihl = header[0] & 0xF
        self.tos = header[1]
        self.len = header[2]
        self.id = header[3]
        self.offset = header[4]
        self.ttl = header[5]
        self.protocol_num = header[6]
        self.sum = header[7]
        self.src = header[8]
        self.dst = header[9]

        # human readable IP addresses
        # 'ipaddress' module's function -> create an IPv4Address or IPv6Address object.
        self.src_address = ipaddress.ip_address(self.src) 
        self.dst_address = ipaddress.ip_address(self.dst)

        # map protocol constants to their names
        self.protocol_map = {1: "ICMP", 6: "TCP", 17: "UDP"}
        try:
            self.protocol = self.protocol_map[self.protocol_num]
        except Exception as e:
            print('%s No protocol for %s' % (e, self.protocol_num))
            self.protocol = str(self.protocol_num)

class ICMP:

    def __init__(self, buff):
        header = struct.unpack('<BBHHH', buff)
        self.type = header[0]
        self.code = header[1]
        self.sum = header[2]
        self.id = header[3]
        self.seq = header[4]

# this sprays out UDP datagrams with our magic message
def udp_sender():
    # Create a UDP socket
    with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as sender:
        # Iterate over the hosts within the subnet
        for ip in ipaddress.ip_network(SUBNET).hosts():
            # Send the message to each IP address
            sender.sendto(bytes(MESSAGE, 'utf8'), (str(ip), 65212))
            
class Scanner:
    def __init__(self, host):
        self.host = host
        if os.name == 'nt':
            socket_protocol = socket.IPPROTO_IP
        else:
            socket_protocol = socket.IPPROTO_ICMP
        self.socket = socket.socket(socket.AF_INET,
                                    socket.SOCK_RAW, socket_protocol)
        self.socket.bind((host, 0))
        self.socket.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)
        if os.name == 'nt':
            self.socket.ioctl(socket.SIO_RCVALL, socket.RCVALL_ON)

    def sniff(self):
        hosts_up = set([f'{str(self.host)} *'])
        try:
            while True:
                # read a packet
                raw_buffer = self.socket.recvfrom(65535)[0]
                # create an IP header from the first 20 bytes
                ip_header = IP(raw_buffer[0:20])
                # if it's ICMP, we want it
                if ip_header.protocol == "ICMP":
                    offset = ip_header.ihl * 4
                    buf = raw_buffer[offset:offset + 8]
                    icmp_header = ICMP(buf)
                    # check for TYPE 3 and CODE
                    if icmp_header.code == 3 and icmp_header.type == 3:
                        if ipaddress.ip_address(ip_header.src_address) in ipaddress.IPv4Network(SUBNET):
                            # make sure it has our magic message
                            if raw_buffer[len(raw_buffer) - len(MESSAGE):] == bytes(MESSAGE, 'utf8'):
                                tgt = str(ip_header.src_address)
                                if tgt != self.host and tgt not in hosts_up:
                                    hosts_up.add(str(ip_header.src_address))
                                    print(f'Host Up: {tgt}')
        # handle CTRL-C
        except KeyboardInterrupt:
            if os.name == 'nt':
                self.socket.ioctl(socket.SIO_RCVALL, socket.RCVALL_OFF)
            print('\\nUser interrupted.')
            if hosts_up:
                print(f'\\n\\nSummary: Hosts up on {SUBNET}')
            for host in sorted(hosts_up):
                print(f'{host}')
            print('')
            sys.exit()

if __name__ == '__main__':
    if len(sys.argv) == 2:
        host = sys.argv[1]
    else:
        host = '192.168.1.203' # substitude with your machine's IPv4 address
    s = Scanner(host)
    time.sleep(5)
    t = threading.Thread(target=udp_sender)
    t.start()
    s.sniff()
```

The code above defines a simple string signature that will be used to test if the responses are coming from UDP packets that were sent originally. The `udp_sender` function takes in a subnet specified at the top of the script, iterates through all IP addresses in that subnet, and sends UDP datagrams to them.

Then, the `Scanner` class is defined, which takes a host as an argument. It initializes by creating a socket, turning on promiscuous mode if running on Windows, and making the socket an attribute of the Scanner class.

The `sniff` method sniffs the network, keeps track of which hosts are up, and performs checks to make sure that the ICMP response is coming from within the target subnet and has the magic string in it. If all checks pass, the IP address of the host where the ICMP message originated is printed.

When the sniffing process is ended by using CTRL-C, the keyboard interrupt is handled by turning off promiscuous mode if on Windows and printing out a sorted list of live hosts.

In the `__main__` block, the Scanner object is created, the `udp_sender` function is spawned in a separate thread to ensure that it doesn't interfere with the ability to sniff responses, and the sniff method is called after waiting for a few seconds.

This script can be used to perform network scanning using ICMP packets and can be run in the command line by typing `python Scanner.py <host>`, where `<host>` is the IP address of the host to listen on. If no host is specified, the script will listen on the default host `192.168.1.203`.