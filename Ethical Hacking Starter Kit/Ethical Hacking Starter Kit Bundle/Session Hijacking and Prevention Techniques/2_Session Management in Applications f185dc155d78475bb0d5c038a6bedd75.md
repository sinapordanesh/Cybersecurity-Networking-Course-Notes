# 2_Session Management in Applications

# Introduction to HTTP

## Session Management in Applications

![Screenshot 2023-05-29 at 1.54.02 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_1.54.02_PM.png)

![Screenshot 2023-05-29 at 1.54.39 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_1.54.39_PM.png)

# Types of HTTP Session

![Screenshot 2023-05-29 at 2.01.23 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_2.01.23_PM.png)

## Some Cookie Features

Chrome saves several types of cookie features, including:

- Name: The name of the cookie.
- Content: The value of the cookie.
- Domain: The domain that set the cookie.
- Path: The path on the domain that the cookie applies to.
- Expires/Max-Age: The date/time that the cookie expires.
- Size: The size of the cookie.
- HTTP: Whether the cookie is an HTTP-only cookie.
- Secure: The cookie is secure (only sent over HTTPS).

## Type of Cookies

### HTTP Cookies

HTTP cookies are small pieces of data that are sent from a website and stored on a user's computer by the user's web browser. Cookies are often used to store information about the user's preferences, login information, and browsing history.

![Screenshot 2023-05-29 at 2.05.57 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_2.05.57_PM.png)

### Session ID in URL

One way to manage sessions is to include the session identifier in the URL. This approach is not recommended, as it can be a security risk, as the session ID may be exposed in the browser's history or in server logs.

![Screenshot 2023-05-29 at 2.07.42 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_2.07.42_PM.png)

### Session ID in Hidden Field

Another way to manage sessions is to include the session identifier in a hidden field in a form. This approach is more secure than including the session ID in the URL, but it still has some potential security risks, such as cross-site scripting attacks.

![Screenshot 2023-05-29 at 2.09.00 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_2.09.00_PM.png)

# Introduction to Network Protocols - Part 1

![Screenshot 2023-05-29 at 2.15.02 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_2.15.02_PM.png)

`SYN = Synchronize Sequence Number`

![Screenshot 2023-05-29 at 2.45.09 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_2.45.09_PM.png)

# Introduction of Network Protocols - Part 2

## Telnet

Telnet is a network protocol used to establish a connection between two computers on a network. It is often used for remote access to servers and other devices. However, it is considered to be an insecure protocol, as data is transmitted in plain text, making it vulnerable to interception and eavesdropping. Therefore, it is recommended to use more secure protocols, such as SSH, instead of Telnet.

![Screenshot 2023-05-29 at 2.48.56 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_2.48.56_PM.png)

## DNS

DNS stands for Domain Name System. It is a protocol used for translating human-readable domain names into IP addresses that computers can understand. When a user types a domain name into their web browser, the browser sends a DNS query to a DNS server to find the IP address associated with that domain name. Once the IP address is found, the browser can connect to the web server hosting the website associated with that domain name.

![Screenshot 2023-05-29 at 3.00.38 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_3.00.38_PM.png)

## IP Address

An IP address is a unique identifier assigned to each device on a network. It is used to route data packets between devices on the network. IPv4 addresses consist of four numbers between 0 and 255, separated by periods. IPv6 addresses are longer and consist of eight groups of four hexadecimal digits, separated by colons.

![Screenshot 2023-05-29 at 3.02.55 PM.png](2_Session%20Management%20in%20Applications%20f185dc155d78475bb0d5c038a6bedd75/Screenshot_2023-05-29_at_3.02.55_PM.png)