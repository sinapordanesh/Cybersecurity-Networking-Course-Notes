# 3_Exploring, Scanning and Enumeration

## Importance of Network Scanning

Network scanning is the process of discovering assets such as devices within an organization's network. This process can be automated using software tools. Network scanning is commonly used to perform asset inventory management.

Network and security professionals use network scanning to determine if there are any rogue or unauthorized devices on their networks. This helps them to ensure that all devices on the network are authorized and accounted for.

In addition, network scanning helps security professionals to determine whether there are unused service ports or running services on a system. This information is crucial for maintaining the security of the network and ensuring that all devices are properly configured and secured.

Overall, network scanning is an essential tool for network and security professionals who want to ensure the security and integrity of their networks.

Network scanning helps security professionals to determine if there are any security vulnerabilities on the devices within their network infrastructure.

Network scanning provides an attacker's view to the network, allowing the network and security professional to determine whether there are any unintentionally exposed assets.

### Banner Grabbing

Banner Grabbing is a technique used by both threat actors and cybersecurity professionals to collect information about a host on a network. This technique enables the determination of open ports and associated running services for those open ports.

Banner Grabbing helps to determine the version of the service that is running on the opened port, which allows for the discovery of potential security vulnerabilities on the service.

### What is Enumeration?

Enumeration is a technique used by both threat actors and cybersecurity professionals to collect information on a target system, specifically on how to gain access to the system and its resources. Enumeration helps threat actors and cybersecurity professionals to collect usernames, passwords, open service ports, and a list of files available on network shares.

### Nmap Enumeration Lab

### `nmap -sn 172.30.1.0/24 --exclude 172.30.1.20`

The command `nmap -sn 172.30.1.0/24 --exclude 172.30.1.20` is used for network scanning. This command will scan the network with the IP range of 172.30.1.0/24, excluding the IP address 172.30.1.20. The `-sn` flag specifies a ping scan, which determines whether hosts are up and running on the network.

### `sudo nmap -sV -sT -A 172.30.1.22`

The command `sudo nmap -sV -sT -A 172.30.1.22` is used for network scanning. The `sudo` command is used to execute the `nmap` command with elevated permissions. The `-sV` flag specifies a service version detection scan. This scan attempts to determine the version of the service running on the scanned port. The `-sT` flag specifies a TCP connect scan. This scan is used to determine whether the port is open or not. The `-A` flag specifies an aggressive scan, which combines several other types of scans, such as OS detection, version detection, and script scanning. The IP address `172.30.1.22` is the target of the scan.

### `nmap 172.30.1.22 --script=smb-os-discovery`

The command `nmap 172.30.1.22 --script=smb-os-discovery` is used for network scanning. This command will scan the network for the IP address `172.30.1.22` and use the `smb-os-discovery` script to attempt to determine the operating system of the target system by sending specially crafted packets to the SMB service on the target system. This technique can be useful for identifying the types of vulnerabilities that may exist on a target system and for determining the appropriate mitigation strategies.

## Hands-on Network Scanning with Nmap

Nmap (Network Mapper) is a free and open-source network scanner that is used by cybersecurity professionals to discover live systems on a network, scan for open TCP and UDP ports, perform banner grabbing, and service enumeration. Nmap also has the capability of detecting the host operating systems and common security vulnerabilities.

The command `nmap -A -T4 -p- 172.30.1.37` is used for network scanning. This command will scan the IP address `172.30.1.37` using the following options:

- `A`: This option enables aggressive scanning, which includes OS detection, version detection, script scanning, and traceroute.
- `T4`: This option sets the timing template to aggressive, meaning that Nmap will send packets as fast as possible without causing network congestion or being detected as an attacker. A higher number increases the speed of the scan.
- `p-`: This option tells Nmap to scan **all** ports, from 1 to 65535.

In summary, this command will perform an aggressive scan on all ports of the IP address `172.30.1.37`. 

### `sudo nmap -S 172.30.1.10 -e eth1 172.30.1.38`

The `sudo nmap` part of the command is used to execute Nmap with elevated permissions. This is necessary to perform certain types of scans that require higher privileges.

The `-S` flag specifies the source IP address for the scan. In this case, the source IP address is `172.30.1.10`. This flag allows you to spoof the source IP address of the packets sent during the scan, which can be useful for bypassing certain types of network security measures.

The `-e` flag specifies the network interface to use for the scan. In this case, the network interface is `eth1`. This flag allows you to specify the network interface that Nmap should use for sending packets during the scan. This can be useful if you have multiple network interfaces on your system.

The IP address `172.30.1.38` is the target of the scan. This is the IP address that Nmap will scan for open ports and other information.

Overall, this command will scan the network for open ports on the target system using the specified source IP address and network interface. It is a useful command for network and security professionals who need to perform detailed network scans and investigations.

### `sudo nmap -A <ip>`

The command `sudo nmap -A <ip>` is used for network scanning. The `sudo` command is used to execute the `nmap` command with elevated permissions. The `-A` flag specifies an aggressive scan, which combines several other types of scans, such as OS detection, version detection, and script scanning. The IP address `<ip>` is the target of the scan, and Nmap will attempt to discover as much information about the target system as possible. This command is useful for network and security professionals who need to perform detailed network scans and investigations.

## MS17-010 Vulnerability

MS17-010 is a critical security flaw in Microsoft Windows that affects the SMB protocol. It can be exploited by attackers to execute code remotely on an affected system, as was the case in the WannaCry ransomware attack in May 2017. Network and security professionals should take appropriate measures to protect their systems.

## MS17-010 Vulnerability

MS17-010 is a critical security flaw in Microsoft Windows that affects the SMB protocol. It can be exploited by attackers to execute code remotely on an affected system, as was the case in the WannaCry ransomware attack in May 2017. Network and security professionals should take appropriate measures to protect their systems.

One way to exploit the MS17-010 vulnerability using Nmap scripts is by running the following command: `nmap -p445 --script smb-vuln-ms17-010 <ip>`.

The `nmap` command is used to execute the scan, with the `-p` flag specifying the port number for the SMB service (port 445). The `--script` flag is used to specify the Nmap script to use for the scan, which is `smb-vuln-ms17-010`. The `<ip>` address is the target of the scan.

This script attempts to exploit the MS17-010 vulnerability by sending a specially crafted packet to the SMB service on the target system. If the vulnerability exists and is not patched, the script may be able to execute code remotely on the target system.

It is important to note that attempting to exploit a vulnerability without proper authorization is illegal and unethical. Network and security professionals should only perform vulnerability scans and penetration tests with the explicit permission of the organization's management.

## Explanation of `sudo nmap --script vuln <ip>` command

The `sudo nmap --script vuln <ip>` command is used for vulnerability scanning. The `sudo` command is used to execute the `nmap` command with elevated permissions. The `--script vuln` flag specifies that Nmap should use scripts that detect vulnerabilities during the scan. The IP address `<ip>` is the target of the scan. This command is useful for network and security professionals who need to perform vulnerability scans and investigations. It is important to note that attempting to exploit a vulnerability without proper authorization is illegal and unethical. Network and security professionals should only perform vulnerability scans and penetration tests with the explicit permission of the organization's management.