# 12_Nmap for Reconnaissance

# Nmap Traceroute Scan

**`Syntax: nmap <target-ip> <-traceroute>`**

- You can scan a target by simply giving an IP address and specifying the traceroute flag
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -traceroute`

# Nmap Trace Traffic & Geo Resolution

**`Syntax: nmap <target-ip> <—script=traceroute-geolocation>`**

- You can scan a target by simply giving an ip address and specifying the traceroute-geolocation.se and identify the geolocation.
- You can add -v to see verbose output
- Eg: **`nmap 192.168.43.213 -traceroute-geolocation.nse`**

Geo resolution is the process of identifying the geographic location of an IP address or domain name. In the case of Nmap, the traceroute-geolocation script can be used to identify the location of targets being scanned.

# Nmap DNS Bruteforce

**`Syntax: nmap <target-ip> ←-script=dns-brute.nse>`**

- You can scan a target by simply giving an ip address and specify the `dns-brute.nse` which will give us the DNS Servers results & Hosted Apps on the server if any
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -dns-brute.nse`

# Nmap Whois Scan

**`Syntax: nmap <target-ip> <—-script=whois-ip, whoisdomain>`**

- You can scan a target by simply giving an IP address and specifying the `whois-ip` script, this will identify information about the target.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -whois-ip,whoisdomain`

# Nmap Robots File Scan

**`Syntax: nmap <target-ip> <--script=http-robots.txt>`**

- You can scan a target by simply giving an IP address and specifying the `http-robots.txt`, this will give you the directories which are allowed and disallowed.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -http-robots.txt`

# Nmap WAF Detect

**`Syntax: nmap <target-ip> <—script=http-waf-detect>`**

- You can scan a target by simply giving an ip address and specifying the `http-waf-detect`
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -http-waf-detect`

# Nmap WAF Fingerprint

**`Syntax: nmap <target-ip> <--script=http-waf-fingerprint>`**

- You can scan a target by simply giving an ip address and specifying the `http-waf-fingerprint`
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -http-waf-fingerprint`

# Wafw00f vs Nmap Scan

**`Syntax: wafwoof <target.com>`**

Syntax: nmap <target-ip> <-script=http-waf-fingerprint>

- You can scan a target by simply giving an IP address and specifying the `http-waf-fingerprint`
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -http-waf-fingerprint`

**Wafw00f** is a tool used to identify the Web Application Firewall (WAF) in use on a website. It works by analyzing the HTTP response from a web server and identifying specific headers or behavior that indicates the presence of a WAF. It can also attempt to identify the specific type of WAF in use.

In contrast, **Nmap** is a more general-purpose network scanning tool that can be used for many different purposes, including identifying open ports, detecting operating systems, and identifying specific services running on a network. However, Nmap also includes a number of specialized scripts that can be used for more specific purposes, such as identifying WAFs.

# Nmap Firewall Detect Firewalled Ports

**`Syntax: nmap <target-ip> <—script=firewalk --traceroute>`**

- You can scan a target by simply giving an ip address and specifying the `firewalk --traceroute`
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -firewalk --traceroute`

# Nmap Email Enumeration

`**Syntax: nmap <target-ip> <--script=http-grep>**`

- You can scan a target by simply giving an ip address and specifying the `http-grep`
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 --script=http-grep.builtins=e-mail`

# Nmap Sitemap Generation Scan

**`Syntax: nmap <target-ip> <--script=http-sitemap-generator>`**

- You can scan a target by simply giving an ip address and specifying the `http-sitemap-generator`
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 -script=http-sitemap-generator`

# Nmap Crawler Tester Scan

`**Syntax: nmap <target-ip> <—script=http-useragent-tester>**`

- You can scan a target by simply giving an ip address and specifying the `http-useragent-tester` to test which crawlers are allowed to crawl the target.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -script=http-useragent-tester`

![Screenshot 2023-06-01 at 4.14.44 PM.png](12_Nmap%20for%20Reconnaissance%20dd3b3a12604648888b3923ffc8562584/Screenshot_2023-06-01_at_4.14.44_PM.png)

A crawler is a program used by search engines to systematically browse and index websites on the internet.

A crawler scan is a type of scan used to determine which web crawlers are allowed to access a target. This can be useful for identifying potential vulnerabilities in a website's security, as well as determining which search engines may be able to index the site. The `http-useragent-tester` script can be used with Nmap to conduct a crawler scan.

# Nmap Discovering Directories Scan

**`Syntax: nmap <target-ip> <—script=http-enum>`**

- You can scan a target by simply giving an ip address and specify the `http-enum` to test which are the sensitive directories on the target which may give some juicy information.
- You can add -v to see verbose output
- Eg: `nmap 192.168.43.213 --script=http-enum`

# Dirsearch Directories Bonus

`**python3 dirsearch.py -u <target> -e php,zip, aspx, env, xml, bak, conf**`

This is a command to run the Dirsearch tool, which is used for discovering directories and files on a web server. The command syntax is `python3 dirsearch.py -u <target> -e php,zip, aspx, env, xml, bak, conf`.

The `-u` flag specifies the target URL to scan, and the `-e` flag specifies the file extensions to search for. In this case, the extensions are php, zip, aspx, env, xml, bak, and conf.