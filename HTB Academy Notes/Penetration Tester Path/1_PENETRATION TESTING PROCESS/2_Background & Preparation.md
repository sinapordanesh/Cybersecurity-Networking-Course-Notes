# 2_Background & Preparation

# Penetration Testing Overview

A `Penetration Test` (`Pentest`) is an organized, targeted, and authorized attack attempt to test IT infrastructure and its defenders to determine their susceptibility to IT security vulnerabilities. 

• `A pentest aims to uncover and identify ALL vulnerabilities in the systems under investigation and improve the security for the tested systems.`

## ****Risk Management****

The main goal of IT security risk management is to identify, evaluate, and mitigate any potential risks that could damage the confidentiality, integrity, and availability of an organization's information systems and data and reduce the overall risk to an acceptable level.

## ****Vulnerability Assessments****

`Vulnerability analysis` is a generic term that can include vulnerability or security assessments and penetration tests.

Systems are checked against known issues and security vulnerabilities by running scanning tools like [Nessus](https://www.tenable.com/products/nessus), [Qualys](https://www.qualys.com/apps/vulnerability-management/), [OpenVAS](https://www.openvas.org/), and similar.

## ****Testing Methods****

An essential part of the process is the starting point from which we should perform our pentest. Each pentest can be performed from two different perspectives:

- `External` or `Internal`

### ****External Penetration Test****

Many pentests are performed from an external perspective or as an anonymous user on the Internet.

### ****Internal Penetration Test****

In contrast to an external pentest, an internal pentest is when we perform testing from within the corporate network.

## ****Types of Penetration Testing****

| Type | Information Provided |
| --- | --- |
| Blackbox | Minimal. Only the essential information, such as IP addresses and domains, is provided. |
| Greybox | Extended. In this case, we are provided with additional information, such as specific URLs, hostnames, subnets, and similar. |
| Whitebox | Maximum. Here everything is disclosed to us. This gives us an internal view of the entire structure, which allows us to prepare an attack using internal information. We may be given detailed configurations, admin credentials, web application source code, etc. |
| Red-Teaming | May include physical testing and social engineering, among other things. Can be combined with any of the above types. |
| Purple-Teaming | It can be combined with any of the above types. However, it focuses on working closely with the defenders. |

## ****Types of Testing Environments****

| Network | Web App | Mobile | API | Thick Clients |
| --- | --- | --- | --- | --- |
| IoT | Cloud | Source Code | Physical Security | Employees |
| Hosts | Server | Security Policies | Firewalls | IDS/IPS |

# Laws and Regulation

Each country has specific federal laws which regulate computer-related activities, copyright protection, interception of electronic communications, use and disclosure of protected health information, and collection of personal information from children, respectively.

It is essential to follow these laws to protect individuals from `unauthorized access` and `exploitation of their data` and to ensure their privacy.

| Categories | USA | Europe | UK | India | China |
| --- | --- | --- | --- | --- | --- |
| Protecting critical information infrastructure and personal data | https://www.cisa.gov/resources-tools/resources/cybersecurity-information-sharing-act-2015-procedures-and-guidance (CISA) | https://gdpr-info.eu/ (GDPR) | https://www.legislation.gov.uk/ukpga/2018/12/contents/enacted | https://www.indiacode.nic.in/bitstream/123456789/13116/1/it_act_2000_updated.pdf | https://digichina.stanford.edu/work/translation-cybersecurity-law-of-the-peoples-republic-of-china-effective-june-1-2017/ |
| Criminalizing malicious computer usage and unauthorized access to computer systems | https://www.justice.gov/jm/jm-9-48000-computer-fraud (CFAA) | https://www.enisa.europa.eu/topics/cybersecurity-policy/nis-directive-new (NISD) | https://www.legislation.gov.uk/ukpga/1990/18/contents | https://www.indiacode.nic.in/bitstream/123456789/13116/1/it_act_2000_updated.pdf | https://www.chinalawtranslate.com/en/2015nsl/ |
| Prohibiting circumventing technological measures to protect copyrighted works | https://www.congress.gov/bill/105th-congress/house-bill/2281 (DMCA) | https://www.europarl.europa.eu/cmsdata/179163/20090225ATT50418EN.pdf |  |  | https://www.omm.com/resources/alerts-and-publications/alerts/what-companies-need-to-know-about-the-chinese-anti-terrorism-law/?sc_lang=zh-CN |
| Regulating the interception of electronic communications | https://www.congress.gov/bill/99th-congress/house-bill/4952 (ECPA) | https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32002L0058 | https://www.legislation.gov.uk/ukpga/1998/42/contents (HRA) | https://legislative.gov.in/sites/default/files/A1872-01.pdf |  |
| Governing the use and disclosure of protected health information | https://aspe.hhs.gov/reports/health-insurance-portability-accountability-act-1996 (HIPAA) |  | https://www.legislation.gov.uk/ukpga/2006/48/contents | https://legislative.gov.in/sites/default/files/A1860-45.pdf |  |
| Regulating the collection of personal information from children | https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa (COPPA) |  | https://www.legislation.gov.uk/ukpga/2016/25/contents/enacted (IPA) |  |  |
| A framework for cooperation between countries in investigating and prosecuting cybercrime |  |  | https://www.legislation.gov.uk/ukpga/2000/23/contents (RIPA) |  |  |
| Outlining individuals' legal rights and protections regarding their personal data |  |  |  | https://www.congress.gov/bill/116th-congress/senate-bill/2889 | https://www.mayerbrown.com/en/perspectives-events/publications/2022/07/china-s-security-assessments-for-cross-border-data-transfers-effective-september-2022 |
| Outlining individuals' fundamental rights and freedoms |  |  |  |  | http://english.www.gov.cn/policies/latestreleases/202108/17/content_WS611b8062c6d0df57f98de907.html |

---

## ****Precautionary Measures during Penetration Tests****

| Obtain written consent from the owner or authorized representative of the computer or network being tested |
| --- |
| Conduct the testing within the scope of the consent obtained only and respect any limitations specified |
| Take measures to prevent causing damage to the systems or networks being tested |
| Do not access, use or disclose personal data or any other information obtained during the testing without permission |
| Do not intercept electronic communications without the consent of one of the parties to the communication |
| Do not conduct testing on systems or networks that are covered by the Health Insurance Portability and Accountability Act (HIPAA) without proper authorization |

# Penetration Testing Process

- A penetration testing process is defined by successive steps and events performed by the penetration tester to find a path to the predefined objective.

## ****Pre-Engagement****

`Pre-engagement` is educating the client and adjusting the contract.

- `Non-Disclosure Agreement`
- `Goals`
- `Scope`
- `Time Estimation`
- `Rules of Engagement`

## ****Information Gathering****

`Information gathering` describes how we obtain information about the necessary components in various ways.

## ****Vulnerability Assessment****

Once we get to the `Vulnerability Assessment` stage, we analyze the results from our `Information Gathering` stage, looking for known vulnerabilities in the systems, applications, and various versions of each to discover possible attack vectors.

## ****Penetration Testing Stages****

### ****Exploitation****

In the `Exploitation` stage, we use the results to test our attacks against the potential vectors and execute them against the target systems to gain initial access to those systems.

### ****Post-Exploitation****

At this stage of the penetration test, we already have access to the exploited machine and ensure that we still have access to it even if modifications and changes are made.

### ****Lateral Movement****

Lateral movement describes movement within the internal network of our target company to access additional hosts at the same or a higher privilege level.

### ****Proof-of-Concept****

In this stage, we document, step-by-step, the steps we took to achieve network compromise or some level of access.

### ****Post-Engagement****

During post-engagement, detailed documentation is prepared for both administrators and client company management to understand the severity of the vulnerabilities found.

## ****Importance****

| Stage | Description |
| --- | --- |
| 1. Pre-Engagement | The first step is to create all the necessary documents in the pre-engagement phase, discuss the assessment objectives, and clarify any questions. |
| 2. Information Gathering | Once the pre-engagement activities are complete, we investigate the company's existing website we have been assigned to assess. We identify the technologies in use and learn how the web application functions. |
| 3. Vulnerability Assessment | With this information, we can look for known vulnerabilities and investigate questionable features that may allow for unintended actions. |
| 4. Exploitation | Once we have found potential vulnerabilities, we prepare our exploit code, tools, and environment and test the webserver for these potential vulnerabilities. |
| 5. Post-Exploitation | Once we have successfully exploited the target, we jump into information gathering and examine the webserver from the inside. If we find sensitive information during this stage, we try to escalate our privileges (depending on the system and configurations). |
| 6. Lateral Movement | If other servers and hosts in the internal network are in scope, we then try to move through the network and access other hosts and servers using the information we have gathered. |
| 7. Proof-of-Concept | We create a proof-of-concept that proves that these vulnerabilities exist and potentially even automate the individual steps that trigger these vulnerabilities. |
| 8. Post-Engagement | Finally, the documentation is completed and presented to our client as a formal report deliverable. Afterward, we may hold a report walkthrough meeting to clarify anything about our testing or results and provide any needed support to personnel tasked with remediating our findings. |