# 8_Nmap OS Detection

# Nmap OS Detection

**`Syntax: nmap <target-ip> <-o>`**

- You can scan a target by simply giving an ip address and specify the `-o` flag which is used for OS version detection and it will identify the operating system on the target system
, You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 - 0`

To use Nmap to scan `scanme.nmap.org` for operating system information, run the following command:

```
nmap scanme.nmap.org -O -v -Pn

```

This command will use Nmap to perform an operating system detection scan on `scanme.nmap.org`. The `-O` flag specifies that the operating system detection feature should be used. The `-v` flag enables verbose output, and the `-Pn` flag tells Nmap to **skip the ping scan** and assume that the host is up.

# Nmap OS Detection Max-retries

## OS Detection

**`Syntax: nmap <target-ip> <--max-os-tries>`**

- You can scan a target by simply giving an ip address and specify the -max-os-retries flag which is used for OS version detection and it will identify the operating system on the target system where you can limit the no of retries you want Nmap to do.
- By Default Nmap tries for 5
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -max-os-tries 1 -v`

# Nmap OS Detection Scan Limit

## OS Detection

**`Syntax: nmap <target-ip> <--osscan-limit >`**

- You can scan a target by simply giving an ip address and specify the - oscan-limit which will limit the scans for targets. And will only perform OS
Detection when map finds at least 1 TCP Open Port.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -oscan-limit -v`

# Namp OS Detection Fuzzy

Nmap's OS detection feature also supports a fuzzy mode, which can be used to detect operating systems that are similar to known operating systems, but not identical. To use this feature, add the `--osscan-guess` flag to your Nmap command. This will allow Nmap to make an educated guess about the operating system based on the information it has gathered during the scan.

# Nmap OS Detection Script

**`Syntax: map <target-ip> <--script --smb-os-discovery >`**

- You can scan a target by simply giving an ip address and specify the
- smb-os-discovery flag which is used for OS version detection and it will identify the operating system on the target system
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -smb-os-discovery -v`

The `-smb-os-discovery` flag is used for OS version detection for targets that have the Server Message Block (SMB) protocol enabled. It allows Nmap to identify the operating system on the target system. Verbose output can be enabled with the `-v` flag.