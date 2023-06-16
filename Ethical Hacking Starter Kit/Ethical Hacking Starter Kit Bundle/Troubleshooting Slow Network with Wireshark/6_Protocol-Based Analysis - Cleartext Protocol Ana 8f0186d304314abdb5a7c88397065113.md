# 6_Protocol-Based Analysis - Cleartext Protocol Analysis

# TCP Analysis - Three-Way Handshake

## The RFC Documents

- What is RFC?
O RFC stands for Request for Comments. It is a document series and a standardization process for internet protocols and technologies. The Internet Engineering Task Force (IETF) and the Internet Society (ISOC) are the organizations that manage the FC process.
- RFCs are technical and organizational documents that describe the design, behavior, and operation of internet protocols and technologies. They are the primary means by which the IETF and the ISOC document and standardize internet protocols and technologies.

## Transmission Control Protocol

- TCP is a transport-layer protocol that provides reliable, ordered, and error-checked delivery of data between applications running on hosts in a packet-switched network, such as the Internet.
- It is connection-oriented, meaning that a virtual connection must be established
between the two endpoints before data can be exchanged.
- TCP uses a sliding window flow control mechanism to regulate the amount of data hat can be sent at one time.
- This allows the receiving host to control the amount of data that the sender can transmit and helps to prevent congestion in the network.
- TCP also includes mechanisms to ensure reliable data transfer, such as the retransmission of lost packets and the detection of duplicate packets.

![Screenshot 2023-06-06 at 12.48.30 PM.png](6_Protocol-Based%20Analysis%20-%20Cleartext%20Protocol%20Ana%208f0186d304314abdb5a7c88397065113/Screenshot_2023-06-06_at_12.48.30_PM.png)

## Investigating TCP-Based Conversation

Right click on a row

![Screenshot 2023-06-06 at 12.50.41 PM.png](6_Protocol-Based%20Analysis%20-%20Cleartext%20Protocol%20Ana%208f0186d304314abdb5a7c88397065113/Screenshot_2023-06-06_at_12.50.41_PM.png)

Stream index is a number assigned to each TCP conversation. It **groups** together all packets that belong to **a** **conversation**. `tcp.stream == 0` filter shows packets of TCP conversation with a stream index of 0 and `tcp.stream == 1` shows packets of TCP conversation with a stream index of 1, and so on.

![Screenshot 2023-06-06 at 1.03.38 PM.png](6_Protocol-Based%20Analysis%20-%20Cleartext%20Protocol%20Ana%208f0186d304314abdb5a7c88397065113/Screenshot_2023-06-06_at_1.03.38_PM.png)

# Identify Hosts: DHCP, NetBIOS, and Kerberos

## DHCP

DHCP automatically assigns IP addresses and other network configuration settings to devices on a network. DHCP servers respond to requests with an IP address and other info, like subnet mask, default gateway, and DNS server addresses. It simplifies network configuration and management in home and enterprise networks.

![Screenshot 2023-06-06 at 1.12.02 PM.png](6_Protocol-Based%20Analysis%20-%20Cleartext%20Protocol%20Ana%208f0186d304314abdb5a7c88397065113/Screenshot_2023-06-06_at_1.12.02_PM.png)

To filter for DHCP option 3 in Wireshark, use the filter `**dhcp.option.dhcp == 3**`. This will show you all DHCP packets that contain the `**Router**` option, which is used to specify the default gateway for the client.

To filter for DHCP option 2 in Wireshark, use the filter `**dhcp.option.dhcp == 2**`. This will show you all DHCP packets that contain the `Time Offset` option, which is used to specify the time zone offset for the client.

## NetBIOS

NetBIOS is a protocol used by Windows-based computers to share resources over a local area network (LAN). It stands for Network Basic Input/Output System. NetBIOS provides services related to the session layer of the OSI model, allowing applications on different computers to communicate over the network. It is often used for file and printer sharing, as well as other network services. However, NetBIOS is an older protocol and is not as widely used today as it once was.

To filter for NetBIOS Name Service (NBNS) traffic in Wireshark, use the filter `**nbns**`. This will show you all packets that use the NBNS protocol, which is used by Windows-based computers to resolve NetBIOS names to IP addresses.

## Kerberos

Kerberos is a network authentication protocol that provides secure communication between client-server applications over an insecure network. It uses a ticket-based system to authenticate users and services, allowing users to access network resources without transmitting their passwords in plain text. Kerberos is widely used in enterprise environments, particularly in Microsoft Windows networks.

# FTP Analysis

FTP is a client-server protocol for transferring files between hosts over a network. To analyze FTP traffic in Wireshark, use the filter `**ftp**`. FTP is an unencrypted protocol, so it is recommended to use a more secure protocol for transferring sensitive data.

- ASCII mode
- Binary mode

→ Security flaws 

### Filters

The Wireshark filter for `ftp.request.command == "USER"` will show all FTP packets that contain a `USER` command request. This filter can be used to identify FTP login attempts, as the `USER` command is used to specify the username for **authentication**. Other options:

- `USER` and PASS: for **authentication**
- `PWD`: to **display** the **current working directory** on the server
- `CWD`: to **change** the **current working directory** on the server
- `LIST`: to **display** a **list of files** in the current directory on the server
- `RETR`: to **download** a **file** from the server
- `STOR`: to **upload** a **file** to the server
- `DELE`: to **delete** a **file** on the server
- `QUIT`: to **close** the FTP **session**
- `CHMOD` : to show all FTP packets that contain a `CHMOD` command request

FTP response codes indicate the status of FTP commands. Use the Wireshark filter `ftp.response.code ==` followed by the three-digit code to see packets with that response code. For example, `ftp.response.code == 150` shows packets with response code 150, indicating transfer starting. Change the number to filter for specific response codes.

- `ftp.response.code == 150`: Data connection already open; transfer starting
- `ftp.response.code == 226`: Closing data connection; transfer complete
- `ftp.response.code == 421`: Service not available, closing control connection
- `ftp.response.code == 550`: Requested action not taken; file unavailable (e.g., file not found, no access)
- `ftp.response.code == 553`: Requested action not taken; file name not allowed
- `ftp.response.code == 530`: Not logged in; authentication failed

`ftp.stream eq 0` is a Wireshark filter that shows only packets belonging to the first TCP conversation in the FTP session. This can be used to focus on the specific packets that relate to the first data transfer in the session, which can be useful for troubleshooting and analysis.

# HTTP Analysis - Log4j Attacks

## HTTP Response Codes

- HTTP Response Codes are important when analyzing network traffic because they provide information about the outcome of a client's request and the status of the communication between the client and the server.
- They can be used to identify and troubleshoot issues with web applications, such as broken links, authentication failures, and server errors.

### HTTP filters

- `http.response.code == 200`: Indicates a successful response.
- `http.response.code == 301`: Indicates a permanent redirect.
- `http.response.code == 302`: Indicates a temporary redirect.
- `http.response.code == 400`: Indicates a bad request.
- `http.response.code == 401`: Indicates unauthorized access.
- `http.response.code == 403`: Indicates forbidden access.
- `http.response.code == 404`: Indicates the requested resource was not found.
- `http.response.code == 500`: Indicates an internal server error.

To filter for HTTP packets based on the user agent in Wireshark, use the filter `http.user_agent`. This will show you all HTTP packets that contain a user agent field, which is used to identify the client application making the request. You can further refine the filter by specifying a specific user agent, such as `http.user_agent == "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3"`. This will show you all HTTP packets that contain the specified user agent string. 

To filter for HTTP packets containing both "jndi:ldap" in the user agent string and a POST request method in Wireshark, use the filter `**http.request.method == "POST" and http.user_agent matches "jndi:ldap"**`. This will show you all HTTP packets that contain a POST request method and the "jndi:ldap" string in the user agent field.