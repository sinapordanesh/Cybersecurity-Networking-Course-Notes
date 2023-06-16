# 14_Nmap Firewall and IDS Dypass

# Nmap Clock Scan with Decoys

**`Syntax: nmap «target-ip> <-D>`**

- You can scan a target by simply giving an ip address and specifying the `-D` Flag.
- Decoy Scan will make you anonymous and use some other IP address to scan the target network.
- For Eg- You can use Google's ip to scan the victim.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 --script=smtp-open-relay`

## Example

```bash
Decoy Scan:
iptables -I INPUT -p tcp -j LOG --log-prefix "AttackerNmap"—log-level=4
nmap -D 216.58.203.164 192.168.0.103
tail -f /var/log/sys log
```

This code is for performing a "Decoy Scan" on a target network. This means that instead of using the attacker's own IP address, it uses decoy IP addresses to make it harder to detect the attack.

The first line creates a log entry for any incoming TCP traffic with a log prefix of "AttackerNmap".

The second line runs the Nmap tool with the `-D` flag, which specifies a list of decoy IP addresses to use in the scan. In this case, it is using the IP address of Google's server (216.58.203.164) as the decoy. The IP address of the actual target network is 192.168.0.103.

The third line uses the `tail` command to monitor the system log in real-time for any new log entries.

# Nmap Select Interface

**`Syntax: nmap <target-ip> <-e ethO>`**

- You can scan a target by simply giving an ip address and specify the `-e`flag to select the interface and choose the adapter you want to use for scanning the target.
- For Eg- You can use use any other adapter to scan the victim.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -script=-e ethO`

# Nmap Spoof MAC Address

**`Syntax: nmap <target-ip> <--spoof-mac>`**

- You can scan a target by simply giving an ip address and specify the spoof-mac flag to spoof the Mac address and stay anonymous.
- For Eg- You can use spoof Mac address to scan the victim.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 --script=spoof-mac`

## Example

```bash
Spoofing the MAC Address:
Specify MAC address from a Vendor → -spoof-mac Dell/Apple/ 3Com
Generate a random MAC address → -spoof-mac 0
Specify your own MAC address → -spoof-mac 00:01:02:25:56: AE
nmap -sT -Pn --spoof-mac Dell 00:01:02:25:56:AE 192.168.1.103
```

This section explains how to spoof a MAC address when performing a scan using Nmap. There are three ways to specify the MAC address:

- Specify a MAC address from a vendor using the `spoof-mac` flag followed by the vendor name (e.g. `Dell`, `Apple`, `3Com`).
- Generate a random MAC address by using the `spoof-mac 0` flag.
- Specify your own MAC address using the `spoof-mac` flag followed by the MAC address (e.g. `00:01:02:25:56:AE`).

An example command that uses the `-spoof-mac` flag is:

```
nmap -sT -Pn --spoof-mac Dell 00:01:02:25:56:AE 192.168.1.103
```

This command spoofs the MAC address to appear as if it's from Dell, and uses the specified MAC address to perform the scan on the target with IP address `192.168.1.103`.

# Nmap Modify Sources Port Scan

**`Syntax: nmap <target-ip> <--source-port 7890>`**

- You can scan a target by simply giving an ip address and specify the `source-port 7890` flag to select the source port you want to use for scanning the target.
- For Eg- You can use use any custom port to scan the victim.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 --script=-source-port 7890`

# Nmap Fake TTK

**`Syntax: nmap <target-ip> <--ttl 128>`**

- You can scan a target by simply giving an ip address and specify the -ttl 128 flag to select the custom ttl value you want to use for scanning the target.
- For Eg- You can use use any custom ttl value to scan the victim.
- You can add -v to see verbose output
- Eg : nmap 192.168.43.213 —script=-ttl 128

# Nmap Relay Proxies

**`Syntax: nmap <target-ip> <--proxies proxy:port>`**

- You can scan a target by simply giving an ip address and specify the `proxies proxy:port` flag to select the custom proxies you want to use for scanning the target.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -script=-proxies proxy:port`

# Nmap Bogus TCP/UDP Checksum

**`Syntax: nmap <target-ip> <—badsum>`**

- This scan induces the deployment of an invalid TCP/UDP/SCT checksum for packets transmitted to our target. As practically every host IP stack would correctly drop the packets, each response accepted is possibly originating from a firewall or Intrusion Detection System that wasn't concerned with confirming the checksum
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -script=-badsum`

# Nmap Fragment Scan

**`Syntax: nmap <target-ip> <-f>`**
• The `-f` command induces our scan to deploy diminutive fragmented IP packets. Specifically, our command utilizes 16 bytes per fragment which diminishes the number of fragments. Fragmented packets is one of them and consist in sending several tiny packets instead of one normal size packet.
. You can add -v to see verbose output
• Eg: `nmap 192.168.43.213 -f`

# Nmap MTU Scan

**`Syntax: nmap <target-ip> <-mtu 8>`**

Nmap is giving the option to the user to set a specific MTU (Maximum Transmission Unit) to the packet.This is similar to the packet fragmentation technique that we have explained above.During the scan that size of the map will create packets with size based on the number that we will give.In this example we gave the number 24 so the map will create 24. byte packets causing a confusion to the firewall. Have in mind that the MTU number must be a multiple of 8 (8,16,24,32 etc. You can specify the MTU of your choice with the command -mtu number target.

- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -f`

```bash
Nmap MTU IP Address Scan:
MTU should be multiple of 8 (8,16,24,32 etc).
nmap --mtu 24 localhost -v
```

This code is for performing an Nmap scan with specific MTU (Maximum Transmission Unit) size. The MTU size determines the size of packets that will be sent during the scan. In this example, the MTU is set to 24, which means that packets of size 24 bytes will be sent. This can cause confusion for the firewall and can lead to false positives.

The `--mtu` flag is used to specify the MTU size and `localhost` is the target IP address. The `-v` flag is used to enable verbose output.

#