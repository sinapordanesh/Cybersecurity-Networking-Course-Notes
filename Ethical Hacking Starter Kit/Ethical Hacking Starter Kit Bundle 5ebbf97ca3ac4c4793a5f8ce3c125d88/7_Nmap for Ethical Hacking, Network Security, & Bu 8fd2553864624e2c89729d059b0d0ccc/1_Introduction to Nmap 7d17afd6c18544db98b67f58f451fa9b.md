# 1_Introduction to Nmap

# Introduction to Nmap

## Nmap

- Network Basics
- What is Nmap
- Why Nmap is important for us
- Nmap Installation
- Network and Port Scans
- Vulnerabilities Scan
- Advance Exploitation
- Breakdown using Wireshark of each packet
- Anatomy of NSE
- Writing Custom NSE Scripts
- Network Mapper - A fast and reliable Network and Port Scanner
- Created by Gordon Lyon
- First Released in 1997 followed by getting better with each update
- Initially build for linux, then ported to all other major distributions like windows, OS X and BSD

## Network Mapper Highlights

- A Fast and reliable Network & Port Scanner
- Free and Opensource
- Powerful Scanning, Vulnerabilities Analysis, Exploitation
- Scan and Enumerate Network Devices
- Enumerate Live Hosts
- Banner Grabbing and Version Detection
- Perform Port Knocking
- A Powerful Nmap Scripting Engine

## Who uses Nmap

- Nmap is simple and powerful and can be used by who wants to do network devices scanning.
- Used widely by Penetrating Testers, Network Administrators, Security Auditors
- Anyone in person who wants to scan and detect vulnerabilities in own systems or target machines
- A Tool for everyone

## What can be achieved by Nmap?

- Security Audits of Firewall
- Open Ports Identification
- Network Scan Audits
- Network Mapping, Network Inventory, Asset Management
- Vulnerability Detection and Exploitation
- Host / Service Uptime Monitoring

# Legal Consideration

## Legal Considerations

- The official documentation of map has an amazing write-up about the legal issues involved with port scanning, available at [https://nmap.org/book/legal-issues.html](https://nmap.org/book/legal-issues.html)
- Things you should keep in mind while scanning :-
    1. Different Countries implies different rules
    2. Safest way is to scan the networks you own or you have exploit permissions

### Is port scanning legal?

- It is legal if :
    1. you are the owner of the network and systems
    2. You have explicit permissions for scanning the network and systems

### Can be Considered illegal incase :

- You do not have permissions to scan the network
- You are not the owner of the network
- You degrade someone's availability of network and systems

# TCP IP and OSI Model

- What are these Models?
- Internet works on this model
- What is TCP IP
- What is OSI
- TCP IP vs OSI Model
- Data Flow in OSI Model
- How de we implement OSI in our daily life

![Screenshot 2023-05-31 at 2.41.33 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_2.41.33_PM.png)

![Screenshot 2023-05-31 at 2.41.58 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_2.41.58_PM.png)

# OSI Model in Day-to-Day Life

![Screenshot 2023-05-31 at 2.53.00 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_2.53.00_PM.png)

![Screenshot 2023-05-31 at 2.53.55 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_2.53.55_PM.png)

# TCP IP vs. OSI Model

![Screenshot 2023-05-31 at 2.56.10 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_2.56.10_PM.png)

## OSI MODEL

- OS stands for Open System Interconnection it shows how information from a software application in one computer moves through a physical medium to the software application in another computer.
- OSI consists of seven layers
- It is developed by ISO (International Standard Organization)

## ТСР IP

- The TCP/IP model general guidelines for how computers and devices will work over a network
- TCP/IP provides end-to-end connectivity on data to be formatted, addressed, transmitted, routed and received at the destination.
- It is developed by ARPANET (Advanced Research Project Agency Network).

# TCP UDP Fundamentals and 3-way Handshake

## What are TCP and UDP

- What is TCP
- What is UDP
- TCP vs UDP
- TCP and UDP Packet Breakdown
- TCP 3-way Handshake

## ТСР

- TCP stands for Transmission Control Protocol
- Connection Oriented Protocol
- Gives Acknowledgement
- Slower compared to UDP
- Example: Email Communication

## UDP

- UDP stands for User datagram Protocol
- Connection Less Protocol
- Doesn't give Gives Acknowledgement
- Faster compared to TCP
- Example: Video Conferencing, Vol

![Screenshot 2023-05-31 at 3.00.05 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.00.05_PM.png)

![Screenshot 2023-05-31 at 3.00.37 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.00.37_PM.png)

![Screenshot 2023-05-31 at 3.01.35 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.01.35_PM.png)

# What is Internet, Intranet, and Extranet

## What is Internet

- The Internet is a globally-connected network of computers that enables people to share information and communicate with each other

# What is Intranet

- An intranet, on the other hand, is a local or restricted network that enables people to store, organize, and share information within an organization

## What is Extranet

- An extranet is a web portal that is accessible by an organization and its external vendors, partners, customers, or any other users that require access to restricted information

## Break it Down

![Screenshot 2023-05-31 at 3.03.54 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.03.54_PM.png)

# Network Types Fundamentals

## Network

![Screenshot 2023-05-31 at 3.05.53 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.05.53_PM.png)

### The purpose of a network is to :

- Share files
- Electronic communication
- Exchange resources

### The network can be linked through:

- Telephone lines
- Radio waves
- Satellites
- Infrared light beams

## LAN

- LAN: Local area network is a collection of computers connected with each other in a small places such as school, hospital, apartment, organisation etc.
- LAN is secure because there is no outside connection with the local area network thus the data which is shared is safe on the local area network and is no accessible by the outside world
- LAN can be a wired connection using cables or it can be wireless
- Due to its small size lan is faster

## MAN

- MAN is a collection of LAN through telephone lines
- The size of the Metropolitan area network is larger than LANs and smaller than WANs(wide area networks),
- MANs cover the larger area of a city or town.

## WAN

- WAN: Wide area network provides long-distance transmission of data.
The size of the WAN is larger than LAN and MAN.
- WAN can cover a country, continent or even a whole world.
- It connects the whole world.
- Example - Internet

## PAN

- A personal area network (PAN) is a computer network for interconnecting electronic devices centred on an individual person's workspace.
- A PAN provides data transmission among devices such as computers, smartphones, tablets and personal digital assistants.
- Examples: Bluetooth, Wifi HotSpot and Zigbee

## CAN

- A Campus area network (CAN) is a computer network for interconnecting electronic devices which are connected inside a campus type of infrastructure.
- Example: LAN in Campus

## SAN

- A Storage area network (SAN) is a computer network for interconnecting electronic devices which are used for storage type within a centralized network
- Example: Secure Storage for Intranet Network

## VPN

- A Virtual Private Network (VPN) is a computer network for creating encrypted tunnels for communication which is a private network
- Example: VPN to connect to a secure network area, NASA

# Network Topologies Fundamentals

## BUS

![Screenshot 2023-05-31 at 3.10.46 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.10.46_PM.png)

## STAR

![Screenshot 2023-05-31 at 3.11.39 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.11.39_PM.png)

## RING

![Screenshot 2023-05-31 at 3.12.09 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.12.09_PM.png)

## HYBRID

- Contains all the types of Topologies

![Screenshot 2023-05-31 at 3.12.46 PM.png](1_Introduction%20to%20Nmap%207d17afd6c18544db98b67f58f451fa9b/Screenshot_2023-05-31_at_3.12.46_PM.png)

# IP and Mac Address Fundamentals

## What is IP

- The IP address is a type of logical address which is used to identify computer devices on the internet
- Full-Form: Internet Protocol Address
- Types: IPv4 IPv6
- Denoted by: Dotted Decimal
- Who gave? Internet Service Provider provides IP Address.
- State: Keeps changing

## What is MAC

- MAC address is a type of physical address which is used to identify computer devices on the internet
- Full-Form : Media Access Control
- Denoted by: Hexa Decimal
- Who gave? NIC Card's Manufacturer provides the MAC Address.
- State: Doesn't Change is fixed. Although can be spoofed

## Pv4 vs Ipv6

- 1981
- IPv4 has a 32-bit address length
- Representation: Dotted
Decimal
- No of Address: 2^32

- 1999
- IPv6 has a 128-bit address length
- Representation: Dotted
Decimal
- No of Address: 2^128

# Ports and Protocols Fundamentals

- A protocol is a set of rules by definition in computer
- Networking protocol is a standard way for computers to exchange information each protocol has a port number assigned to it
- There are total 65535 ports 2^16 -1 = 65536-1 = 65535