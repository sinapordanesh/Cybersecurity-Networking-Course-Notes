# 9_Nmap Output Formats

## Save Normal Output to File

**`Syntax: nmap <target-ip> <-oN file.txt>`**

- You can scan a target by simply giving an ip address, specifying the -oN flag, and saving the output in a normal format in a file for later use.
- You can add -v to see verbose output
- Eg : `map 192.168.43.213 -oN normal.txt`

# Nmap XML Output

## Save XML Output to File

**`Syntax: nmap <target-ip> <-oX file.txt>`**

- You can scan a target by simply giving an ip address and specify the `-oX` flag which is used to save the output in the XML Format in a file for later use.
- You can add `-v` to see verbose output
- Eg: `nmap 192.168.43.213 -oX mIfile.txt`
- Saving output xmI to html sitproc

# Nmap XML to HTML Output

This command is used to convert an Nmap XML output file to HTML using the `xsltproc` utility. The resulting HTML file will be named sina.html.

```bash
xsltproc nmapxmloutput.xml nmapoutputhtml.html > sina.html
```

# Nmap XML to CSV for Recon

`**Syntax: nmap <target-ip> <-oX file.txt>**`

- Parsing the XML Output to CS Format for Penetration Testing and Bug Bounty
Hunting Recon Phase
- **`Python parsey.py op.xml op.csv`**

**`python nmap-xml-to-csv.py example.xml > sina.csv`**

This command is used to parse the Nmap XML output file to CSV format for penetration testing and bug bounty hunting recon phase.

# Nmap Greppable Output

## Save "Grep"able Output to File

`**Syntax: nmap <target-ip> <-oG file. txt>**`

- You can scan a target by simply giving an ip address and specify the `-oG` flag which is used for saving the output in grepable format for later use.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -oG grepablefile.txt`

**Grepable** format is a format that can be easily used with the Unix tool `grep`. It is a simple text format that lists each port and its state and can be used for further processing with other tools and scripts.

# Nmap Script Kiddie Output

**Script Kiddie** is an unskilled individual who uses pre-made scripts/programs to attack computer systems and networks. Nmap's script kiddie output format is a simplified version of the normal output, listing open ports/services and potential vulnerabilities/security risks in an easy-to-read format for non-technical users.

## ScRipT K1dd3 Output to File

**Syntax: map <target-ip> <-oS file. txt›**

- You can scan a target by simply giving an ip address and specify the `-oS` flag which is used for Script Kiddie Output and save it to a file for later use.
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -oS scRipTKiDdie.txt`

# Nmap All Outputs

## Save All Types Output to File

`**Syntax: nmap <target-ip> <-oA file.txt>**`

- You can scan a target by simply giving an ip address and specify the `-oA` flag which is used for saving all types of output to a file for later use
- You can add -v to see verbose output
- Eg : `nmap 192.168.43.213 -oA alloutputsfile`
    
    It will create all file formats with base name as alloutputsfile