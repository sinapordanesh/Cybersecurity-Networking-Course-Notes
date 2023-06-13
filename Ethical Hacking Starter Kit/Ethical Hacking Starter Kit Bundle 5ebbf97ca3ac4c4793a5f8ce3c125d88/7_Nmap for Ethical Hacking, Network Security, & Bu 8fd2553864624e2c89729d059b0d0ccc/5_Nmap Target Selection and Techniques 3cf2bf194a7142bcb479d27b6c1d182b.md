# 5_Nmap Target Selection and Techniques

# Namp IP address and Host Scan

## Scanning an IP

`**Syntax: nmap <target-ip>**`

- You can scan a target by simply typing the target IP and nmap will start scanning for default 1000 ports
- You can add -v to see verbose output

## Scanning a HOST

`**Syntax: nmap <www.example.com>**`

- You can scan a target by simply typing the hostname (www.example.com) and n will start scanning for **default** **1000** ports.
- You can add -v to see verbose output

# Nmap IP Range Scan

## Scanning a range of IPs

**`Syntax: nmap <ip-address-range>`**

- You can scan a target by simply typing the IP address and range specification (192.168.43.**213-250**) and Nmap will start scanning for default 1000 ports
- You can add `-v` to see **verbose output**

## Scanning a Subnet

**`Syntax: nmap <ip-address/24>`**

- You can scan a target by simply typing the IP address and Subnet and Nmap will start scanning for all the IP's/Hosts in the subnet for default 1000 ports
- You can add `-v` to see **verbose output**
- Comparison with Netdiscover

# Nmap Host Subnet Scan

## IP Calculation

`ipcalc` is a command-line tool used to calculate various IP address parameters. It can be used to calculate subnet masks, network addresses, broadcast addresses, and more.

Using `ipcalc` can be useful when determining the IP addresses in a subnet that need to be scanned with Nmap.

- To use it, type `ipcalc` followed by the IP address and subnet mask you wish to calculate.
- Some useful flags include:
    - `h` to display help information
    - `n` to suppress the network portion of the output
    - `p` to suppress the prefix length portion of the output
    - `s` to suppress the summary portion of the output

We use `Ipcalc` to find out what are network subnets and the range of IPs under a subnet, then feed Nmap with that information for enumeration.

# Nmap Host Subnet Scan Fast

`nmap {ip} -v -f`

- This command is used for a fast scan of hosts in a subnet.
- The `f` flag is used to enable fragmented scan, which can help bypass firewall rules.
- The `v` flag is used to display verbose output.

# Namp Host Discovery

The command `nmap -sP {ip}` can be used to perform host discovery. This command sends ICMP echo requests to the specified IP address to determine if it is up and running. It can be used to quickly determine which hosts are active on a network.

# Netdiscover vs Nmap

Netdiscover is a command used to perform a network discovery scan. It sends ARP requests to the specified IP range and returns a list of active hosts on the network. This can be a useful first step in a network reconnaissance operation.

On the other hand, Nmap is a command used to perform a verbose scan on a single IP address or a subnet. This will allow you to see detailed information about the open ports on the target devices.

## Netdiscover

`netdiscover -r {ip}` is a command used to perform a network discovery scan. It sends ARP requests to the specified IP range and returns a list of active hosts on the network. This can be a useful first step in a network reconnaissance operation.

![Screenshot 2023-06-01 at 12.15.40 PM.png](5_Nmap%20Target%20Selection%20and%20Techniques%203cf2bf194a7142bcb479d27b6c1d182b/Screenshot_2023-06-01_at_12.15.40_PM.png)

## Nmap

`nmap {ip/subnet} -v` is the command used to perform a verbose scan on a single IP address or a subnet. This will allow you to see detailed information about the open ports on the target devices.

![Screenshot 2023-06-01 at 12.16.00 PM.png](5_Nmap%20Target%20Selection%20and%20Techniques%203cf2bf194a7142bcb479d27b6c1d182b/Screenshot_2023-06-01_at_12.16.00_PM.png)

# Arpscan vs Nmap

Arpscan is a command used to discover hosts on a network by using ARP. It sends out ARP requests to all hosts on a network and then collects the responses. It is a fast way to discover hosts on a local network.

To use it, type `arp-scan -I {interface} {ip-range}`. Replace `{interface}` with the name of the network interface you want to use (e.g. eth0), and replace `{ip-range}` with the range of IP addresses you want to scan (e.g. 192.168.0.0/24). You can add the `-l` flag to display the results in a list format.

Arpscan can be useful for quickly discovering hosts on a network, but it does not provide as much detailed information about the hosts as Nmap does.

# Nmap Large Target/Input List Scan

## Scanning Targets from a Text File
**`Syntax: nmap -iL <list.txt>`**

- You can scan a target by simply giving a list of targets you want to scan (list.txt) a map will start scanning for default 1000 ports
- You can add -v to see verbose output
1. Type `nano list.txt` to create a new file named "list.txt" using the Nano text editor.
2. Add one IP address or hostname per line that you want to scan to the input file. Save and close the file.
3. Run the nmap command with the `iL` flag followed by the path to the input file. For example, if your input file is in the current directory, you would run `nmap -iL list.txt`.
4. Nmap will start scanning each target on the list for default 1000 ports. You can add `v` to see verbose output.

**`nmap -iL lisst.txt {-port.ip} - v`**

# Nmap Choose Random Hosts

The command `nmap -iR 10 -v` can be used to choose 10 random hosts and perform a verbose scan on them. The `-iR` flag is used to specify the number of random hosts to choose, and the `-v` flag is used to display verbose output.

# Nmap Exclude Host from Network

## `n**map 192.168.43.1/24 - -exclude 192.168.43.213 -v**`

The command `nmap 192.168.43.1/24 --exclude 192.168.43.213 -v` can be used to scan a network and exclude a specific host (192.168.43.213) from the scan. The `-v` flag is used to display verbose output.

# Nmap No Host Discovery Scan / Bypassing Windows Firewall Rule

## Scanning target & Ignore Discovery

**`Syntax: nmap -target-ip <-Pn>`**

- You can scan a target by simply giving a target ip address you want to scan with -Pn flag and map will start scanning for default 1000 ports without Host
Discovery
- Helpful in order to bypass firewalls which blocks PING
- You can add -v to see verbose output

![Screenshot 2023-06-01 at 12.31.33 PM.png](5_Nmap%20Target%20Selection%20and%20Techniques%203cf2bf194a7142bcb479d27b6c1d182b/Screenshot_2023-06-01_at_12.31.33_PM.png)

`**Syntax: nmap -Pn <target-ip> [-p <ports>]**`