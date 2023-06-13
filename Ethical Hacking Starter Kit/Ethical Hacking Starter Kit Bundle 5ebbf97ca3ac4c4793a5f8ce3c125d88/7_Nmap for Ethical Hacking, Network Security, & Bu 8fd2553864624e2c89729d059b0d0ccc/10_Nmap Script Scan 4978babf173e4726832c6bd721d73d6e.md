# 10_Nmap Script Scan

# Nmap Default Script Scan

## Scan using Default Safe Scripts

**`Syntax: nmap <target-ip> <-sC>`**

- You can scan a target by simply giving an ip address and specify the -sC flag which is used for running safe scripts on the target and it will tell about **which services are running on the ports.**
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -sC`

# Nmap Script Help & Usage

## Getting Help with any Scripts

**Syntax: nmap <target-ip> <—script-help=scriptname>**

- You can scan a target by simply giving an ip address and specifying the -script-help flag which is used to identify any script and its usage.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -script-help=scriptnameyouwanthelpfor`

# Nmap Script Arguments

**`Syntax: map <target-ip> <-script=scripiname --script-args>`**

- You can scan a target by simply giving an ip address and specifying the -script-help flag which is used to identify any script and its usage.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -script=scriptname-script-args`

## Example

```bash
nmap —script ftp-brute —script-args userdb=/Users/sina/ nmap/wordlists/usernames.txt,passdb=/Users/sina/nmap/ wordlists/passwords.txt -p 9999 -Pn 192.168.43.213 - sV -v
```

This script is used to perform an FTP brute force attack. It specifies the userdb and passdb arguments to specify the location of the username and password wordlists, respectively. These wordlists are used to try to guess the FTP login credentials. The -p flag is used to specify that the scan should only target port 9999. The -Pn flag is used to disable host discovery, which means that Nmap will not try to ping the target before scanning it. The -sV flag is used to enable version detection, which means that Nmap will try to determine the version of the FTP service running on port 9999. The -v flag is used to enable verbose output, which means that Nmap will print out more detailed information about the scan as it is running.

Copy the script on the terminal directly and run it by itself.

# Nmap NSE Script Scan

## Scan using specific Scripts

**`Syntax: nmap <target-ip> <--script=scriptname.nse>`**

- You can scan a target by simply giving an ip address and specify the script name and nmap will runt the script and will give you the output.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -sV --script=scriptname.nse`

`**nmap --script ftp-brute -p 9999 - Pn 192.168.43.213 - sV -v**`

This is a command to run an FTP brute force attack using the Nmap script `ftp-brute`. The `-p` flag is used to specify that the scan should only target port 9999. The `-Pn` flag is used to disable host discovery, which means that Nmap will not try to ping the target before scanning it. The `-sV` flag is used to enable version detection, which means that Nmap will try to determine the version of the FTP service running on port 9999. The `-v` flag is used to enable verbose output, which means that Nmap will print out more detailed information about the scan as it is running. The IP address of the target is `192.168.43.213`.

# Nmap Scan with Scripts Sets

## Scan using set of Scripts

**`Syntax: nmap <target-ip> <--script "http-*">`**

- You can scan a target by simply giving an ip address and specify the - script="http-** flag which is used for scanning services with the names starting with "http-"
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -script "http-*”`

# Nmap Updating the Database

## Update Script Database

**`Syntax: nmap <target-ip> <--script=updatedb>`**

- You can scan a target by simply giving an ip address and specify the -updatedb flag which is used for updating the DB of map for new scripts.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -script=updated`