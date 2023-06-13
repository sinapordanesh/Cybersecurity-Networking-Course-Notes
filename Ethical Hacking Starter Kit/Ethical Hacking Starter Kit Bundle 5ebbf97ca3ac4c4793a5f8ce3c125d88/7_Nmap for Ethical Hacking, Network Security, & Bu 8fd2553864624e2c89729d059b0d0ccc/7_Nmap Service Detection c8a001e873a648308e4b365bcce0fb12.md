# 7_Nmap Service Detection

# Nmap Service

## Standard Service Detection

**`Syntax: nmap <target-ip> <-sV>`**

- You can scan a target by simply giving an ip address and specify the `-sV` flag which is used for service version detection, it will tell about which services are running on the ports
- You can add `-v` to see verbose output
- Eg: `nmap 192.168.43.213 -sV`

## Light Service Detection

`**Syntax: nmap <target-ip> <-sV --version-intensity 0>**`

- You can scan a target by simply giving an ip address and specify the `-sV` flag which is used for service version detection, it will tell about which services are running on the ports
You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -sV --version-intensity 0`

## Aggressive Service Detection

`**Syntax: map <target-jp> <-sV --version-intensity 5>**`

- You can scan a target by simply giving an ip address and specify the -sV flag which is used for service version detection, it will tell about which services are running on the ports
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -sV --version-intensity 5`

# Nmap Service Version Light

**`nmap 192.168.43.213 -p9999 -v --open -sV --version-light`**

This command is used to scan a target with IP address `192.168.43.213`.

The options used in the command are:

- `p9999`: This option specifies that only port `9999` will be scanned.
- `v`: This option enables verbose output which gives more detailed information about the scan.
- `-open`: This option specifies that only open ports will be scanned.
- `sV`: This option is used for service detection and will give information about which services are running on the open ports.
- `-version-light`: This option limits the number of probes sent to the target, making the scan faster but less accurate.

The output of this command shows that port `9999` is open and running the `PRTG Network Monitor httpd` service. Additionally, it provides information about the MAC address of the scanned device.

# Nmap Service Version Trace

`**nmap 192.168.43.213 -p9999 -V --open -sV - -version-trace**`

This command is used to scan a target with IP address `192.168.43.213`.

The options used in the command are:

- `p9999`: This option specifies that only port `9999` will be scanned.
- `V`: This option enables verbose output which gives more detailed information about the scan.
- `open`: This option specifies that only open ports will be scanned.
- `sV`: This option is used for service detection and will give information about which services are running on the open ports.
- `**version-trace**`: This option increases the verbosity of the output, providing more detailed information about the scan.

The output of this command will show the same information as the previous command, but with more detail about the probes being used and the specific versions of software being detected.