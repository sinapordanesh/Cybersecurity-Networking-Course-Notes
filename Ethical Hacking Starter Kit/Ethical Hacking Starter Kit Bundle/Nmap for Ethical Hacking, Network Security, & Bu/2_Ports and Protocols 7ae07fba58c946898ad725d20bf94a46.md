# 2_Ports and Protocols

# Ports and Protocols: FTP

## File Transfer Protocol

- Port Number: **20,21**
- FTP: File Transfer Protocol
- Use: The purpose of FTP is to transfer files Upload and Download

## Demo

To use FTP, follow these commands:

1. Enter `ftp` in the terminal
2. Type `open {ip}` to connect to the FTP server
3. Enter your username
4. Enter your password

### FTP on Free Live Server

The website "[in.000webhost.com](http://in.000webhost.com/)" is a free web hosting service that allows users to host their own website for free. It is often used for testing and development purposes.  

# Ports and Protocols: SSH

Secure Shell

- Port Number: **22**
- SSH: Secure Shell
- Use: The SSH protocol uses encryption to secure the connection between a client and a server

To execute an SSH command, open a terminal and enter the following command:

```
ssh username@server_address

```

Replace `username` with your username and `server_address` with the address of the server you want to connect to. You will then be prompted to enter your password.

# Ports and Protocols: SSH, Telnet, vs RDP

## Telnet

- Port Number: 23
- Telnet: Telecommunication Network
- Use: Its main function is to establish an unencrypted connection between a server and a remote computer.

## SSH vs Telnet

NOTE:

- The key difference between Telnet and SSH is that SSH uses encryption, which means that all data transmitted over a network is secure from eavesdropping.
- Telnet provides insecure connection which can lead to MIT

## RDP

- Port No - 3389
- RDP:- Remote Desktop Protocol
- This port has been developed by Microsoft. It enables you to establish a connection with a remote computerBut this time you need a windows device at the other end.

# Ports and Protocols: SMTP, POP3, & IMAP4

## SMTP

- Port No - 25
- SMTP:- Simple mail transfer protocol
- Used for **Sending** Emails

## IMAP

- Port No - 143
- IMAP4 :- Internet Message Access Protocol
- Used for **receiving** mails

## How Email Works?

![Screenshot 2023-05-31 at 3.39.50 PM.png](2_Ports%20and%20Protocols%207ae07fba58c946898ad725d20bf94a46/Screenshot_2023-05-31_at_3.39.50_PM.png)

# Ports and Protocols: DNS

## DNS

- Port No - 53
- DNS:- Domain Name Server/Service/System
- URL to IP Mapping and vice versa.
- `google.com -> 216.58.200.174`
- `216.58.200.174 -> google.com`

To use the `ping` command, open a terminal and enter the following command:

```
ping {ip_address}

```

Replace `{ip_address}` with the IP address of the server you want to ping. This command sends packets to the server and measures the time it takes to receive a response. It is often used to test network connectivity and diagnose network issues.

# Ports and Protocols: DHCP

## DHCP

- Port No - 67
- DHCP: Dynamic Host Configuration Protocol
- Assigns IP address to hosts
- DORA Process

![Screenshot 2023-05-31 at 3.45.01 PM.png](2_Ports%20and%20Protocols%207ae07fba58c946898ad725d20bf94a46/Screenshot_2023-05-31_at_3.45.01_PM.png)

### Performing a DHCP Request via Wireshark

1. Open Wireshark and select the network interface you want to capture packets on.
2. Click on the "Capture Options" button and select "DHCP" under the "Capture Filter" tab.
3. Click "Start" to begin capturing DHCP packets.
4. Start a DHCP request on your device by opening the network settings and selecting "Renew DHCP Lease" or a similar option.
5. Observe the DHCP request and response packets in Wireshark. You should see a **DISCOVER** packet from the **client**, an **OFFER** packet from the **server**, a **REQUEST** packet from the **client**, and an **ACK** packet from the **server**.

# Port and Protocols: HTTP and HTTPs

## НТТР

- Port No - 80
- HTTP :- Hyper Text Transfer Protocol
- This is an application layer protocol
- Connect to the web pages on the internet
- Port 80 basically expects or waits for the web client to ask for a connection.
- Once this connection has been made, you will get the privilege to connect to the World Wide Web and get access to various web pages out there.

## HTTPS

- Port No - 443
- HTTP:- Hyper Text Transfer Protocol Secure
- HTTPS is a secure protocol which uses TLS/SSL certificate to ensure the authentication