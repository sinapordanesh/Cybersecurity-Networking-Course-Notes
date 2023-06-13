# 4_Nmap Scan Types and Techniques

# Nmap TCP Scan

Here is a list of some common Nmap scan types and their brief explanations:

- `sS` (SYN scan): Sends SYN packets to determine whether ports are open or closed. This is the default scan type if no others are specified.
- `sT` (TCP connect scan): Completes the TCP three-way handshake to determine whether a port is open.
- `sU` (UDP scan): Sends UDP packets to determine whether a UDP port is open or not.
- `sA` (ACK scan): Sends ACK packets to determine whether a port is filtered or unfiltered.
- `sN` (NULL scan): Sends null packets to determine whether a port is open or closed.
- `sF` (FIN scan): Sends FIN packets to determine whether a port is open or closed.
- `sX` (Xmas scan): Sends Christmas tree packets to determine whether a port is open or closed.
- `sP` (Ping scan): Sends ICMP echo requests to determine whether a host is up or not.

Note that there are many other flags and options available for Nmap scans, but these are some of the most common ones.

## Nmap Scan Types

- SYN
- ACK
- ZOMBIE
- NULL
- XMAS
- ТСР
- UDP
- FIN

## TCP Connect

 `**nmap -sT <target-ip> [-p <ports>**`

- TCP Connect scan completes the 3-way handshake.
- If a port is open, the operating system completed the TCP three-way handshake and the port scanner immediately closes the connection to avoid DOS.
- This is "noisy" because the services can log the sender IP address and might trigger Intrusion Detection Systems.

![Screenshot 2023-05-31 at 4.05.14 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.05.14_PM.png)

![Screenshot 2023-05-31 at 4.05.25 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.05.25_PM.png)

- **Pro**: Quite reliably scans TCP ports
- **Cons**: less "stealthy" (connection attempts will be logged by the server), takes a longer time, sends more packets

# Nmap TCP Stealth Scan

## TCP SYN ("Stealth"/"Half-Open")

 **`nmap -sS <target-ip> [-p <ports>]`**

- This scan type is also known as "half-open scanning" because it never actually opens a full TCP connection.
- The port scanner generates an SYN packet. If the target port is open, it will respond with an SYN-ACK packet. The scanner host responds with an RST packet, closing the connection before the handshake is completed. ie: Only 2 steps of 3way handshake happens
- If the port is closed but unfiltered, the target will instantly respond with an
RST packet

![Screenshot 2023-05-31 at 4.09.44 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.09.44_PM.png)

![Screenshot 2023-05-31 at 4.09.56 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.09.56_PM.png)

- **Pro**: Quicker because sends less no of packets
- **Cons**: With advancements in firewall and server defenses technology, it is not stealthy anymore

# Nmap NULL Scan

## NULL Scan

 **`nmap -sN <target-ip> [-p <ports>`**

- Another very stealthy scan that sets all the TCP header flags to off or null.
- This is not normally a valid packet and some hosts will not know what to do with this. Windows operating systems are in this group, and scanning them with NULL scans will produce unreliable results.
- However, for non-Windows servers protected by a firewall, this can be a way to get through.
- Null scan: no flags set
- If a RST packet is received, the port is considered closed, while no response means it is open | filtered. The port is marked filtered if an
ICMP unreachable error

![Screenshot 2023-05-31 at 4.16.43 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.16.43_PM.png)

![Screenshot 2023-05-31 at 4.16.51 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.16.51_PM.png)

- **Pro**: Stealthy can bypass some firewalls
- **Cons**: Unreliable at many times

# Nmap UDP Scan

## UDP

 **`nmap -sU «target-ip> [-p <ports>]`**

- UDP Scanning utilises UDP and IMP packets to discover the status of a port.
- Nmap sends an empty UDP packet and either receives no reply or an ICMP
Port Unreachable packet.
- But due to UDP's connectionless nature, the output can be unreliable at times.

![Screenshot 2023-05-31 at 4.20.54 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.20.54_PM.png)

![Screenshot 2023-05-31 at 4.21.09 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.21.09_PM.png)

![Screenshot 2023-05-31 at 4.21.29 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.21.29_PM.png)

## Interesting Scenario

Port status "open|filtered" instead of "open" or "close"?

Here's why:

- When Nmap received no reply from port, one scenario could be that port 88 and 138 really is open, and is therefore not responding with any reply, however, another possible scenario is that a firewall is filtering out our traffic and thus the UDP packet never reaches the target and we receive no reply.
- Either way, we won't know the difference - which results in Nmap displaying "open|filtered".

**Pro**: Allows the scanning of UDP ports
**Cons**: Unreliable at many times

# Nmap FIN Scan

## FIN Scan

**`nmap -sF <target-ip> [-p <ports>`**

- Another **very stealthy** scan that sets all the TCP header flags to FIN
- Stealthily sneak through stateless firewalls and packet filters, by turning on different TCP flags like FIN
- However, for non-Windows servers protected by a firewall, this can be a way to get through.
- FIN scan: FIN Flag Set

Note: If a port is closed, it replies with a RST-ACK and if it is open, it reply with FIN

![Screenshot 2023-05-31 at 4.28.21 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.28.21_PM.png)

![Screenshot 2023-05-31 at 4.28.33 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.28.33_PM.png)

![Screenshot 2023-05-31 at 4.29.09 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.29.09_PM.png)

- **Pro**: **Stealthy** can **bypass** some **firewalls** and packet filters
- **Cons**: Unreliable at many times

# Nmap XMAS Scan

## XMAS Scan

 **`nmap -sX <target-ip> [-p <ports>]`**

- Another very **stealthy** scan that sets all the TCP header flags to FIN,URG,PSH
- Stealthily sneak through stateless firewalls and packet filters, by turning on different TCP flags like FIN,URG,PSH
- However, for non-Windows servers protected by a firewall, this can be a way to get through.
- XMAS scan: FIN, URG, PSH Flag Set
- THE Packet lights up like a Christmas tree

Note: If a port is closed, it replies with a RST-ACK and if it is open, it reply with FIN.URG.PSH

![Screenshot 2023-05-31 at 4.33.49 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.33.49_PM.png)

![Screenshot 2023-05-31 at 4.34.26 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.34.26_PM.png)

- **Pro**: Stealthy can bypass some firewalls and packet filters
- **Cons**: Unreliable at many times

# Nmap ACK Scan

# Nmap IDLE or ZOMBIE Scan

## IDLE (Zombie) Scan

 **`nmap -sI <zombie-ip> [-p <ports>] <target-ip>`**

- In this scan we need a "zombie" in order to perform an idle scan.
- In a nutshell, Nmap will attempt to leverage an idle host to indirectly launch a port scan, therefore hiding our IP address from the target.
- It is one of the more controversial options in Nmap since it really only has a use for malicious attacks

![Screenshot 2023-05-31 at 4.38.29 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.38.29_PM.png)

![Screenshot 2023-05-31 at 4.38.43 PM.png](4_Nmap%20Scan%20Types%20and%20Techniques%20938e4532166946bc9f2822fe05dcf17f/Screenshot_2023-05-31_at_4.38.43_PM.png)

- **Pro**: To **Hide** your **identity** and scan hosts A
- **Cons**: typically harder to perform these days as firewalls detects and blocks

# Nmap Scan Types Summary: Revision

| Switch | Description | Example |
| --- | --- | --- |
| -sS | TCP SYN port scan. | map -sS 192.168.1.1 |
| -sT | TCP Connect port scan. | nmap -sT 192.168.1.1 | |
| -sU | UDP port scan. | nmap -sU 192.168.1.1  |
| -sA | TCP ACK port scan. | nmap -sA 192.168.1.1  |
| -sI | TCP IDLE port scan. | nmap -sI 192.168.1.1  |
| -sN | TCP NULL port scan. | nmap -sN 192.168.1.1 |
| -sX | TCP XMAS port scan. | nap -sX 192.168.1.1  |
| -sF | TCP FIN port scan. | nap -sF 192.168.1.1 |