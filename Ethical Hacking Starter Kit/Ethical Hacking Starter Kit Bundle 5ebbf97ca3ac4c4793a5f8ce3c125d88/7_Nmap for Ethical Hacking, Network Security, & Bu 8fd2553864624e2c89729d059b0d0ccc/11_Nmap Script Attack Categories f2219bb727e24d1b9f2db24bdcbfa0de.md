# 11_Nmap Script Attack Categories

# Nmap Safe Script

**`Syntax: nmap ‹target-ip> <-script=safe,default>`**

- You can scan a target by simply giving an ip address and specifying the safe, default flag which is used for scanning targets with default and safe script types.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 --script=safe,default`

# Nmap Vulnerability Scripts

**`Syntax: nmap <target-ip> <--script=vuln>`**

- You can scan a target by simply giving an IP address and specifying the `vuln` flag which is used for scanning targets with `vuln` script types.
- You can add `-v` to see verbose output
- Eg: `nmap 192.168.43.213 --script=vuln`

# Nmap DOS Script

**`Syntax: nmap <target-ip> <--script=dos>`**

- You can scan a target by simply giving an ip address and specify the dos flag which is used for scanning targets with dos script types.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 --script=dos`

# Nmap Exploit Script

**`Syntax: nmap <target-ip> <--script=exploit>`**

- You can scan a target by simply giving an IP address and specifying the exploit flag which is used for scanning targets with exploit script types.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 --script=exploit`

# Nmap Intrusive Script

**`Syntax: nmap <target-ip> <—script=intrusive>`**

- You can scan a target by simply giving an ip address and specify the intrusive flag which is used for scanning targets with intrusive script types.
- You can add -v to see verbose output
Eg: N`map 192.168.43.213 --script=intrusive`

# Nmap Malware Script Scan

**`Syntax: nmap <target-ip> <—script=http-malware-host>`**

- You can scan a target by simply giving an IP address and specifying the exploit flag which is used for scanning targets with exploit script types.
- You can add `-v` to see verbose output
- Eg: `nmap 192.168.43.213 --script=exploit`

# Nmap Not Including Scripts Scan

**`Syntax: map <target-ip› <—-script =not scripttype>`**

- You can scan a target by simply giving an IP address and specifying the not intrusive flag which is used for scanning targets with not intrusive script types.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 --script=not intrusive`

# Nmap Boolean Expression Scan

**`Syntax: nmap <target-ip> <--script=and or not scripttype>`**

- You can scan a target by simply giving an IP address and specifying the and or not script type flag which is used for scanning targets with and or not script type script types.
- You can add -v to see verbose output
- Eg: `**nmap 192.168.43.213 --script=and or not scripttype**`