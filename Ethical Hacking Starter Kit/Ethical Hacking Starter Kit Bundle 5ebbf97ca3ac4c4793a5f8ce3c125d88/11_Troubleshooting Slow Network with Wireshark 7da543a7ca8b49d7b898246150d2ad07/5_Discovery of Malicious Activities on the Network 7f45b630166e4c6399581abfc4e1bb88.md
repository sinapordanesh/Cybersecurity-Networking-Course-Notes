# 5_Discovery of Malicious Activities on the Network

# Discovering of Nmap Scans

![Screenshot 2023-06-05 at 4.33.08 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-05_at_4.33.08_PM.png)

### `**tcp.flags.syn == 1 && tcp.flags.ack == 0**`

To detect **Nmap** scans in Wireshark, apply the filter `tcp.flags.syn == 1 && tcp.flags.ack == 0`. This will show you all packets with the SYN flag set but the ACK flag not set, which is a common indicator of an Nmap scan.

![Screenshot 2023-06-05 at 4.37.30 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-05_at_4.37.30_PM.png)

# Discovery of ARP Poisoning and MITM Attacks

![Screenshot 2023-06-06 at 11.50.26 AM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_11.50.26_AM.png)

![Screenshot 2023-06-06 at 11.51.54 AM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_11.51.54_AM.png)

![Screenshot 2023-06-06 at 11.53.06 AM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_11.53.06_AM.png)

![Screenshot 2023-06-06 at 12.11.12 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_12.11.12_PM.png)

## An ARP poisoning example

![Screenshot 2023-06-06 at 12.12.18 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_12.12.18_PM.png)

![Screenshot 2023-06-06 at 12.12.51 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_12.12.51_PM.png)

![Screenshot 2023-06-06 at 12.13.02 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_12.13.02_PM.png)

## Wireshark warnings page

![Screenshot 2023-06-06 at 12.14.18 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_12.14.18_PM.png)

![Screenshot 2023-06-06 at 12.14.43 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_12.14.43_PM.png)

## An attack type

### ARP Storm Attach → Broadcasting → DOS

Difficult to protect → Right filtering 

![Screenshot 2023-06-06 at 12.16.30 PM.png](5_Discovery%20of%20Malicious%20Activities%20on%20the%20Network%207f45b630166e4c6399581abfc4e1bb88/Screenshot_2023-06-06_at_12.16.30_PM.png)

# Investigating the Anomalous Packets -DNS and ICMP Tunneling

### DNS Tunneling

An example of DNS tunneling is when an attacker wants to exfiltrate data from a compromised network. The attacker creates a DNS query that contains the stolen data, and sends it to a DNS server they control. The DNS server responds with a DNS response that contains the stolen data. The attacker can then easily decode the data from the DNS response.

To implement DNS tunneling, the attacker needs to use a tool that can encode data into DNS queries and responses. There are several open-source tools available for this, such as Iodine and Dnscat2.

To protect against DNS tunneling, network administrators can implement DNS security features such as DNSSEC and DNS filtering. DNSSEC is a protocol that adds digital signatures to DNS queries and responses, making it harder for attackers to modify them. DNS filtering can be used to block DNS queries and responses to known malicious domains.

### ICMP Tunneling

An example of ICMP tunneling is when an attacker wants to bypass a firewall that blocks all traffic except for HTTP. The attacker encodes data in the payload of ICMP packets, and sends them to a server they control. The server then decodes the data and sends it back to the attacker using the same method.

To implement ICMP tunneling, the attacker needs to use a tool that can encode data into ICMP packets. There are several open-source tools available for this, such as Icmpsh and PingTunnel.

To protect against ICMP tunneling, network administrators can implement firewalls that block all ICMP traffic except for the types that are necessary for the network to function properly. They can also use network analysis tools like Wireshark to monitor for anomalies in ICMP traffic.

I hope that helps! Let me know if you have any further questions.

To detect an attack in Wireshark, look for anomalous traffic patterns. For example, if you notice a large number of packets coming from a single IP address, or if you see a lot of traffic to unusual ports or protocols. Additionally, you can use filters to search for specific types of traffic, such as Nmap scans or ARP poisoning attacks.

Here is an example of Wireshark output that might indicate an attack:

```bash
No.     Time           Source             Destination        Protocol  Length
1       0.000000       192.168.1.1        192.168.1.2        TCP       66
2       0.000100       192.168.1.2        192.168.1.1        TCP       66
3       0.001200       192.168.1.3        192.168.1.1        TCP       66
4       0.001300       192.168.1.1        192.168.1.3        TCP       66
5       0.002400       192.168.1.4        192.168.1.1        TCP       66
6       0.002500       192.168.1.1        192.168.1.4        TCP       66

```

In this example, we can see that there is a lot of TCP traffic between 192.168.1.1 and other IP addresses on the network. This could be a sign of an attack, especially if the traffic is to unusual ports or protocols.

To further investigate this traffic, you can apply filters to isolate traffic from a specific IP address or to search for specific protocols or ports. For example, you could apply a filter to show only traffic to port 80, which is commonly used for HTTP traffic.

By using Wireshark to monitor network traffic and search for anomalous patterns, you can detect potential attacks before they cause damage to your network.

#