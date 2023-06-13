# 6_Nmap Port Scan and Techniques

# Nmap Port Scan and Techniques

## Using Nmap to Scan Specific Ports

To scan specific ports, you can use the `-p` option followed by a comma-separated list of port numbers or service names. For example, to scan for FTP and SSH services on a host with IP address 192.168.43.213, you can use the command:

```
nmap 192.168.43.213 -p ftp,ssh -v
```

This will perform a verbose scan of ports associated with the FTP and SSH services on the target host. The `-v` option is used to enable verbose output, which provides more detailed information about the scan.

# Nmap Ports Scanning

`**nmap 192.168.43.213 -p ft,ssh, smtp, 9999,53,80 -v**`

This command will perform a verbose scan of the ports associated with the FTP, SSH, SMTP, and HTTP services, as well as those associated with ports 9999, 53, and 80 on the target host with IP address 192.168.43.213:

# Nmap Scan Open Ports

`**nmap 192.168.43.213 -p- -v --open**`

The following command will perform a verbose scan of all ports on the target host with IP address 192.168.43.213, and will only show open ports.

This command uses the `-p-` option to scan all ports, and the `--open` option to only show open ports. The `-v` option is used to enable verbose output.

`**nmap 192.168.43.97 -p1-200 - v --open**`

This command will perform a verbose scan of all ports **from** 1 **to** 200 on the target host with IP address 192.168.43.97, and will only show open ports.

# Nmap Port Knocking

**`Syntax: for x in 1-10000; do nmap -Pn -p $× server_ip_address; done`**

- Port-knocking the an obfuscation-as-security technique.
- It basically means that after knocking on ports in a specific sequence a certain port will open automatically.
- Useful for identifying ports which are hidden

## Example

**`for × in 1-10000; do nmap -p $× 192.168.43.213; done`**

This command performs a port-knocking scan using Nmap on the target host with IP address 192.168.43.213. The `for` loop iterates over all values of `x` from 1 to 10000, and for each value, the `nmap` command is executed with the current value of `x` as the port to be scanned. The `p` flag specifies the port to be scanned, and the `Pn` flag tells Nmap not to try to ping the host before scanning, which can speed up the scan and prevent false negatives.

- The `p` flag specifies the port or range of ports to be scanned by Nmap.
- The `Pn` flag tells Nmap to not try to ping the host before scanning, which can speed up the scan and prevent false negatives.
- The `do` command is used to execute the `nmap` command with the current value of `x` as the port to be scanned.
- The `for` loop iterates over all values of `x` from 1 to 10000, executing the `nmap` command for each value.

# Nmap Fast Port Scan

**`Syntax: nmap <target-ip> <-F> -v`**

- You can scan a targets Port Numbers using Fast Port Scan, and map will start scanning for TCP and UDP ports
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -F`

# Nmap Quick Save & Append Output

`**nmap 192.168.0.1 - F | grep open | cat >> results. txt**`

The command `nmap 192.168.0.1 -F | grep open I cat >> results.txt` performs a fast port scan on the IP address 192.168.0.1 and outputs the results to the terminal. The `grep` command filters out only the lines that contain the word "open". The `cat` command **appends** the filtered output to the file `results.txt`.

`**nmap 192.168.0.1 - F | grep open | tee > results. txt**`

The `tee` command **saves** the output to the file `results.txt` and also displays it in the terminal.

# Nmap Port Scan No Randomize/Sequential

**`Syntax: nmap <target-ip> <-r> -v`**

- You can scan a targets Port Numbers using No Randomize Port Scan, and map will start scanning for TCP and UDP ports **in** a **sequential** manner.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 **-r**`

# Nmap Top Ports Scan

**`Syntax: nmap <target-ip> <—top-ports N> -v`**

- You can scan a targets Top Port Numbers using -top-port N command, where N stands for **no of ports**,
- For EG - If you want to scan 10 ports you will type 10 instead of N and nap will start scanning for TCP and UDP ports.
- You can add -v to see verbose output
Eg: `map 192.168.43.213 -top-ports N`

# Nmap Ports Ratio Scan

**`Syntax: map <target-ip> <--ports-ratio> -v`**

- You can scan a targets Port Number using Port ratio scan, It Scans all ports in nmap-services file with a ratio greater than the one given.
- You can add -v to see verbose output
Eg: `nmap 192.168.43.213 -ports-ratio`

# Nmap Port Scan Summary Revision

![Screenshot 2023-06-01 at 1.03.25 PM.png](6_Nmap%20Port%20Scan%20and%20Techniques%2096675d3d14a7441fa8c019744e0c7528/Screenshot_2023-06-01_at_1.03.25_PM.png)