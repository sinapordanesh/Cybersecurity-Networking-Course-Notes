# 1_Using Academy Effectively

# Introduction to the Penetration Tester Path

**`Introduction`**

---

1.[Penetration Testing Process](https://academy.hackthebox.com/module/details/90)

---

2.[Getting Started](https://academy.hackthebox.com/module/details/77)

---

**`Reconnaissance, Enumeration & Attack Planning`**

---

3.[Network Enumeration with Nmap](https://academy.hackthebox.com/module/details/19)

---

4.[Footprinting](https://academy.hackthebox.com/module/details/112)

---

5.[Information Gathering - Web Edition](https://academy.hackthebox.com/module/details/144)

---

6.[Vulnerability Assessment](https://academy.hackthebox.com/module/details/108)

---

7.[File Transfers](https://academy.hackthebox.com/module/details/24)

---

8.[Shells & Payloads](https://academy.hackthebox.com/module/details/115)

---

9.[Using the Metasploit Framework](https://academy.hackthebox.com/module/details/39)

---

**`Exploitation & Lateral Movement`**

---

10.[Password Attacks](https://academy.hackthebox.com/module/details/147)

---

11.[Attacking Common Services](https://academy.hackthebox.com/module/details/116)

---

12.[Pivoting, Tunneling, and Port Forwarding](https://academy.hackthebox.com/module/details/158)

---

13.[Active Directory Enumeration & Attacks](https://academy.hackthebox.com/module/details/143)

---

**`Web Exploitation`**

---

14.[Using Web Proxies](https://academy.hackthebox.com/module/details/110)

---

15.[Attacking Web Applications with Ffuf](https://academy.hackthebox.com/module/details/54)

---

16.[Login Brute Forcing](https://academy.hackthebox.com/module/details/57)

---

17.[SQL Injection Fundamentals](https://academy.hackthebox.com/module/details/33)

---

18.[SQLMap Essentials](https://academy.hackthebox.com/module/details/58)

---

19.[Cross-Site Scripting (XSS)](https://academy.hackthebox.com/module/details/103)

---

20.[File Inclusion](https://academy.hackthebox.com/module/details/23)

---

21.[File Upload Attacks](https://academy.hackthebox.com/module/details/136)

---

22.[Command Injections](https://academy.hackthebox.com/module/details/109)

---

23.[Web Attacks](https://academy.hackthebox.com/module/details/134)

---

24.[Attacking Common Applications](https://academy.hackthebox.com/module/details/113)

---

**`Post-Exploitation`**

---

25.[Linux Privilege Escalation](https://academy.hackthebox.com/module/details/51)

---

26.[Windows Privilege Escalation](https://academy.hackthebox.com/module/details/67)

---

**`Reporting & Capstone`**

---

27.[Documentation & Reporting](https://academy.hackthebox.com/module/details/162)

---

28.[Attacking Enterprise Networks](https://academy.hackthebox.com/module/details/163)

# Academy Modules Layout

## Recommended Sequence

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled.png)

## Pre-Engagement

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled%201.png)

The pre-engagement stage is where the main commitments, tasks, scope, limitations, and related agreements are documented in writing

| Path | Description |
| --- | --- |
| Information Gathering | Next, we move towards the Information Gathering stage. Before any target systems can be examined and attacked, we must first identify them. It may well be that the customer will not give us any information about their network and components other than a domain name or just a listing of in-scope IP addresses/network ranges. Therefore, we need to get an overview of the target web application(s) or network before proceeding further. |
- Strong foundation about fundamental modules:
    
    ****1. Learning Process****
    
- In addition, knowledge about **OS's**:
    
    ****2. Linux Fundamentals****
    
    ****3. Windows Fundamentals****
    
- understand how interconnected systems function and communicate:
    
    ****4. Introduction to Networking****
    
- Web applications:
    
    ****5. Introduction to Web Applications****
    
    ****6. Web Requests****
    
    ****7. JavaScript Deobfuscation****
    
- various technologies to facilitate and accelerate remote management of users, systems, and other resources:
    
    ****8. Introduction to Active Directory****
    
    ****9. Getting Started****
    

## ****Information GatheringInformation Gathering****

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled%202.png)

| Path | Description |
| --- | --- |
| Vulnerability Assessment | The next stop on our journey is Vulnerability Assessment, where we use the information found to identify potential weaknesses. We can use vulnerability scanners that will scan the target systems for known vulnerabilities and manual analysis where we try to look behind the scenes to discover where the potential vulnerabilities might lie. |
- Information gathering:
    
    ****10. Network Enumeration with Nmap****
    
    ****11. Footprinting****
    
    ****12. Information Gathering - Web Edition****
    
- through various sources and social media platforms:
    
    ****13. OSINT: Corporate Recon****
    

## ****Vulnerability Assessment****

The vulnerability assessment stage is divided into two areas. On the one hand, it is an approach to scan for known vulnerabilities using automated tools. On the other hand, it is analyzing for potential vulnerabilities through the information found.

- thinking outside the box
- discover gaps

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled%203.png)

| Path | Description |
| --- | --- |
| Exploitation | The first we can jump into is the Exploitation stage. This happens when we do not yet have access to a system or application. Of course, this assumes that we have already identified at least one gap and prepared everything necessary to attempt to exploit it. |
| Post-Exploitation | The second way leads to the Post-Exploitation stage, where we escalate privileges on the target system. This assumes that we are already on the target system and can interact with it. |
| Lateral Movement | Our third option is the Lateral Movement stage, where we move from the already exploited system through the network and attack other systems. Again, this assumes that we are already on a target system and can interact with it. However, privilege escalation is not strictly necessary because interacting with the system already allows us to move further in the network under certain circumstances. Other times we will need to escalate privileges before moving laterally. Every assessment is different. |
| Information Gathering | The last option is returning to the Information Gathering stage when we do not have enough information on hand. Here we can dig deeper to find more information that will give us a more accurate view. |
- ability to analyze:
    
    ****14. Vulnerability Assessment****
    
    ****15. File Transfers****
    
    ****16. Shells & Payloads****
    
    ****17. Using the Metasploit-Framework****
    

## ****Exploitation****

Exploitation is the attack performed against a system or application based on the potential vulnerability discovered during our information gathering and enumeration

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled%204.png)

| Path | Description |
| --- | --- |
| Information Gathering | Once we have initial access to the target system, regardless of how high our privileges are at that moment, we need to gather information about the local system. Whether we use this new information for privilege escalation, lateral movement, or data exfiltration does not matter. Therefore, before we can take any further steps, we need to find out what we are dealing with. This inevitably takes us to the vulnerability assessment stage, where we analyze and evaluate the information we find. |
| Post-Exploitation | Post-exploitation is mainly about escalating privileges if we have not yet attained the highest possible rights on the target host. As we know, more opportunities are open to us with higher privileges. This path actually includes the stages Information Gathering, Vulnerability Assessment, Exploitation, and Lateral Movement but from an internal perspective on the target system. The direct jump to post-exploitation is less frequent, but it does happen. Because through the exploitation stage, we may already have obtained the highest privileges, and from here on, we start again at Information Gathering. |
| Lateral Movement | From here, we can also skip directly over to Lateral Movement. This can come under different conditions. If we have achieved the highest privileges on a dual-homed system used to connect two networks, we can likely use this host to start enumerating hosts that were not previously available to us. |
| Proof-of-Concept | We can take the last path after gaining the highest privileges by exploiting an internal system. Of course, we do not necessarily have to have taken over all systems. However, if we have gained the Domain Admin privileges in an Active Directory environment, we can likely move freely across the entire network and perform any actions we can imagine. So we can create the Proof-of-Concept from our notes to detail and potentially automate the paths and activities and make them available to the technical department. |

The first category is general network protocols often used and present in almost every network:

****18. Password Attacks****

****19. Attacking Common Services****

****20. Pivoting, Tunneling & Port Forwarding****

****21. Active Directory Enumeration & Attacks****

## ****Web Exploitation****

Web exploitation is the second part of the exploitation stage. Many different technologies, improvements, features, and enhancements have been developed in this area over the last few years, and things are constantly evolving:

****22. Using Web Proxies****

****23. Attacking Web Applications with Ffuf****

****24. Login Brute Forcing****

****25. SQL Injection Fundamentals****

****26. SQLMap Essentials****

****27. Cross-Site Scripting (XSS)****

****28. File Inclusion****

****29. Command Injections****

****30. Web Attacks****

****31. Attacking Common Applications****

## ****Post-Exploitation****

After gaining in-depth knowledge about how these operating systems function, we must adapt our techniques to the particular operating system and carefully study how `Linux Privilege Escalation` and `Windows Privilege Escalation` work.

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled%205.png)

| Path | Description |
| --- | --- |
| Information Gathering / Pillaging | Before we can begin escalating privileges, we must first get an overview of the inner workings of the exploited system. After all, we do not know which users are on the system and what options are available to us up to this point. This step is also known as Pillaging. This path is not optional, as with the others, but essential. Again, entering the Information Gathering stage puts us in this perspective. This inevitably takes us to the vulnerability assessment stage, where we analyze and evaluate the information we find. |
| Exploitation | Suppose we have found sensitive information about the system and its' contents. In that case, we can use it to exploit local applications or services with higher privileges to execute commands with those privileges. |
| Lateral Movement | From here, we can also skip directly over to Lateral Movement. This can come under different conditions. If we have achieved the highest privileges on a dual-homed system used to connect two networks, we can likely use this host to start enumerating hosts that were not previously available to us. |
| Proof-of-Concept | We can take the last path after gaining the highest privileges by exploiting an internal system. Of course, we do not necessarily have to have taken over all systems. However, if we have gained the Domain Admin privileges in an Active Directory environment, we can likely move freely across the entire network and perform any actions we can imagine. So we can create the Proof-of-Concept from our notes to detail and potentially automate the paths and activities and make them available to the technical department. |

After we have gained access to a system, we must be able to take further steps from within the system:

****32. Linux Privilege Escalation****

****33. Windows Privilege Escalation****

## ****Lateral Movement****

Lateral movement is one of the essential components for moving through a corporate network. We can use it to overlap with other internal hosts and further escalate our privileges within the current subnet or another part of the network. `Lateral Movement` stage requires access to at least one of the systems in the corporate network.

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled%206.png)

| Path | Description |
| --- | --- |
| Vulnerability Assessment | If the penetration test is not finished yet, we can jump from here to the Vulnerability Assessment stage. Here, the information already obtained from pillaging is used and analyzed to assess where the network services or applications using an authentication mechanism that we may be able to exploit are running. |
| Information Gathering / Pillaging | After a successful lateral movement, we can jump into Pillaging once again. This is local information gathering on the target system that we accessed. |
| Proof-of-Concept | Once we have made the last possible lateral movement and completed our attack on the corporate network, we can summarize the information and steps we have collected and perhaps even automate certain sections that demonstrate vulnerability to the vulnerabilities we have found. |

Since both `Lateral Movement` and `Pillaging` require access to an already exploited system, these techniques and methods are covered in different modules, such as `Getting Started`, `Linux Privilege Escalation`, and `Windows Privilege Escalation`, and many others.

## ****Proof-of-Concept****

The `Proof-Of-Concept` (`POC`) is merely proof that a vulnerability found exists. As soon as the administrators receive our report, they will try to confirm the vulnerabilities found by reproducing them.

![Untitled](1_Using%20Academy%20Effectively%209601b3684a8840dbb858bbd1718e79b4/Untitled%207.png)

| Path | Description |
| --- | --- |
| Post-Engagement | At this point, we can only go to the post-engagement stage, where we optimize and improve the documentation and send it to the customer after an intensive review. |

When we have all information about the vulnerability, need to automate it:

****34. Introduction to Python 3****

## ****Post-Engagement****

The `Post-Engagement` stage also includes cleaning up the systems we exploit so that none of these systems can be exploited using our tools.

reconcile all our notes with the documentation we have written:

****35. Documentation & Reporting****

****36. Attacking Enterprise Networks****

# Academy Exercises & Questions