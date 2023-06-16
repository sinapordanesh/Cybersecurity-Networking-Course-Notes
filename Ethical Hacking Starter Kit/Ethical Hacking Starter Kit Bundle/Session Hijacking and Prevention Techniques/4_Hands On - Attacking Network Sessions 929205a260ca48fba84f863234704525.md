# 4_Hands On - Attacking Network Sessions

# TCP Session - Predicting the sequence

## TCP Predicting Sequence

- TCP Predicting Sequence attack is an attempt to predict the sequence number in a TCP connection, which can be used to forge packets.
- If the attack is successful due to delivery of forged packets, the attacker can inject data into an existing TCP connection or terminate any existing connection using the RST flag.
- In older, vulnerable operating systems, the generation of predictable sequence numbers makes this attack possible.

![Screenshot 2023-05-30 at 4.20.57 PM.png](4_Hands%20On%20-%20Attacking%20Network%20Sessions%20929205a260ca48fba84f863234704525/Screenshot_2023-05-30_at_4.20.57_PM.png)

# UDP Session Hijacking

- UDP doesn't use sequence numbers like TCP Protocol.
- UDP session hijacking works like TCP session hijacking, except UP Protocol is weak that does not use sequence or ACK numbers. Attacker need to forge a server reply to a client UDP request before the server can respond.

## Lab

- To start a netcat listener on port 7777, run the following command:
    
    ```
    nc -vvulp 7777
    
    ```
    
    This will start a listener on port 7777, which means that any incoming traffic on that port will be accepted and can be used for further analysis or exploitation.
    
- To connect to the netcat listener from another machine, run the following command:
    
    ```
    nc -vvnu {ip} 7777
    
    ```
    
    Replace `{ip}` with the IP address of the machine running the netcat listener. This will establish a UDP connection to the listener on port 7777, allowing you to interact with the listener and potentially exploit any vulnerabilities that may exist.
    
- To run Scapy3 on Kali, you can use the following command:
    
    ```
    sudo scapy3
    
    ```
    
- Then:

```bash
i=IP()
i.dst={dest ip}
i.src={src ip}
u=UDP()
u.dport={dst port(7777)}
u.sport={src port}
payload=”message”
packet=i/u/payload
packet.display()
send(packet)
```

1. `i=IP()`: This creates a new IP packet object.
2. `i.dst={dest ip}`: This sets the destination IP address of the packet.
3. `i.src={src ip}`: This sets the source IP address of the packet.
4. `u=UDP()`: This creates a new UDP packet object.
5. `u.dport=7777`: This sets the destination port of the UDP packet to 7777.
6. `u.sport={victim port}`: This sets the source port of the UDP packet to `{victim port}`.
7. `payload=”message”`: This sets the payload of the UDP packet to the string "message".
8. `packet=i/u/payload`: This creates a new packet by combining the IP packet, UDP packet, and payload.
9. `packet.display()`: This displays the contents of the packet.
    
    This code creates a new UDP packet with a specific payload, and sets the source and destination IP addresses and ports. This can be used to simulate a UDP session and test for vulnerabilities or analyze network traffic.
    

## Scenario

![Screenshot 2023-05-30 at 4.40.06 PM.png](4_Hands%20On%20-%20Attacking%20Network%20Sessions%20929205a260ca48fba84f863234704525/Screenshot_2023-05-30_at_4.40.06_PM.png)

# IP Spoofing

- IP spoofing is a technique wherein the attacker sends messages to a computer with an IP address indicating that the message is coming from a trusted host.
- The attacker doesn't need to get in between the communication, nor guess any sequence number, just change the source IP in the Header.
- Common attack purposes are:
    - Attacker hides their source IP
    - Cause DOS/DDOS attack because the devices will respond to the spoofed IP address mentioned as the source
    - Malicious Content Script
    

## `hping3 -S {ip1} -a {ip2} -c 3`

The hping3 command allows you to send custom packets to a target IP address. The `-S` flag indicates that the packets should be sent with the SYN flag set, which can be used to initiate a TCP connection. The `-a` flag allows you to specify a source IP address for the packets. Replace `{ip1}` with the target IP address and `{ip2}` with the spoofed source IP address. The `-c 3` flag specifies that only three packets should be sent.

Example usage:

```
hping3 -S 192.168.1.100 -a 10.0.0.2 -c 3

```

This will send three TCP SYN packets to the IP address `192.168.1.100`, with a source IP address of `10.0.0.2`.

![Screenshot 2023-05-30 at 5.40.02 PM.png](4_Hands%20On%20-%20Attacking%20Network%20Sessions%20929205a260ca48fba84f863234704525/Screenshot_2023-05-30_at_5.40.02_PM.png)

# Telnet Session Hijacking

- Telnet is an interactive and bidirectional message system running on TCP Protocol.
- Telnet will not check the source IP addresses from the received packets. When these protocols get a fake packet from an attacker, they assume that it's a valid one from the connected host and send a reply to the IP set in the fake packet.

# DNS Session Hijacking

- Domain Name Server (DNS) hijacking is a type of DNS attack in which DNS queries are incorrectly resolved to redirect the victim to malicious sites.
- This technique is commonly used in attacks such as Pharming or Phishing.
- Common attack vectors for DNS hijacking include:
    - Local DNS Hijacking
    - Router DNS Hijacking
    - MITM DNS Hijacking
    - Rogue DNS Servers
    

## Lab

DNS session hijacking is when an attacker modifies the hosts file in a victim's operating system to redirect them to a malicious website instead of a legitimate one. The hosts file is a local database that maps hostnames to IP addresses. By adding a new entry to the hosts file, the attacker can redirect the victim to a malicious IP address when they try to visit a legitimate website. This technique is commonly used in attacks such as Pharming or Phishing. To prevent DNS session hijacking, it is recommended to use secure DNS servers, enable DNSSEC, and regularly monitor the hosts file for any unauthorized changes.

To edit the host file folder in **Windows**, navigate to `C:\\Windows\\System32\\drivers\\etc\\hosts`.

To edit the host file folder in **Linux**, navigate to `/etc/hosts`.

To edit the host file folder in **macOS**, navigate to `/private/etc/hosts`.

# ARP Spoofing

# ARP Spoofing

- ARP spoofing is a type of attack where Attacker falsified ARP (Address Resolution Protocol) messages over the network. This results in the linking attacker's MAC address with the IP address of a legitimate computer or server on the network.
- ARP spoofing attacks can only occur on local area networks.
- Common attack vectors are:
    - Denial Of Service
    - Session Hijacking
    - Man-in-the-Middle

## Lab

`ifconfig` is a command-line utility that displays network interface information for your system, including IP addresses, network masks, and MAC addresses. It is commonly used on Unix-based operating systems such as Linux, macOS, and FreeBSD.

`ip link` is a command-line utility used on Linux and Unix-based operating systems to manage network interfaces, including bringing them up or down, setting Ethernet addresses and MTU sizes, and viewing interface information.

The `arp` command on Kali is used to view and modify the Address Resolution Protocol (ARP) cache. The ARP cache is a table that maps IP addresses to MAC addresses. The `arp` command can be used to view the contents of the cache, add new entries, or delete existing ones. Some common `arp` commands are:

- `arp -a`: Displays the contents of the ARP cache.
- `arp -s {ip} {mac}`: Adds a new entry to the ARP cache for the IP address `{ip}` and MAC address `{mac}`.
- `arp -d {ip}`: Deletes the entry for the IP address `{ip}` from the ARP cache.

`Ettercap` is a powerful suite for MITM attacks, able to sniff connections, filter content, and dissect protocols. Install it on Kali with `sudo apt-get install ettercap-graphical`. Use with caution and only on networks you're authorized to analyze.

![Screenshot 2023-05-30 at 6.11.56 PM.png](4_Hands%20On%20-%20Attacking%20Network%20Sessions%20929205a260ca48fba84f863234704525/Screenshot_2023-05-30_at_6.11.56_PM.png)

# SSL Strip

# SSL Strip

- Using MITM attack, adversaries will exploit network capabilities to strip the SSL connection and downgrade it to HTTP.
- This results in a breach in the integrity and confidentiality such as login user credentials, accounts information, etc.
- Primary ways through which SSL Stripping attacks can be executed
    - ARP Spoofing
    - Proxy Server
    - Open Wi-Fi Hotspots

## lab

Set of commands that can be used in a lab to perform network attacks:

1. `sudo bettercap -iface eth0`: This command starts the bettercap tool on the `eth0` interface, allowing you to perform various network attacks such as ARP spoofing, DNS spoofing, and SSL stripping.
2. `set http.proxy.sslstrip true`: This command sets the `http.proxy.sslstrip` parameter to `true`, which can be used to perform SSL stripping attacks.
3. `set net.probe on`: This command enables network probing, which can be used to discover hosts and services on the network.
4. `set net.sniff on`: This command enables network sniffing, which can be used to capture and analyze network traffic.
5. `arp.spoof on`: This command enables ARP spoofing, which can be used to redirect network traffic and perform man-in-the-middle attacks.

Note that these commands are for educational purposes only and should only be used on networks that you are authorized to analyze.