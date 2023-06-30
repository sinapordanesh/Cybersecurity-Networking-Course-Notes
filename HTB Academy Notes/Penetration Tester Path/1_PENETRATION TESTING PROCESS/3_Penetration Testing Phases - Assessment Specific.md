# 3_Penetration Testing Phases - Assessment Specific Stages

# Pre-Engagement

![Untitled](3_Penetration%20Testing%20Phases%20-%20Assessment%20Specific%20f4aa5e95b3cd40948deef651c3b0a221/Untitled.png)

Pre-engagement is the stage of preparation for the actual penetration test. During this stage, many questions are asked, and some contractual agreements are made. The client informs us about what they want to be tested, and we explain in detail how to make the test as efficient as possible.

The entire pre-engagement process consists of three essential components:

1. Scoping questionnaire
2. Pre-engagement meeting
3. Kick-off meeting

### `Non-Disclosure Agreement` (`NDA`):

| Type | Description |
| --- | --- |
| Unilateral NDA | This type of NDA obligates only one party to maintain confidentiality and allows the other party to share the information received with third parties. |
| Bilateral NDA | In this type, both parties are obligated to keep the resulting and acquired information confidential. This is the most common type of NDA that protects the work of penetration testers. |
| Multilateral NDA | Multilateral NDA is a commitment to confidentiality by more than two parties. If we conduct a penetration test for a cooperative network, all parties responsible and involved must sign this document. |
- Sample (not exhaustive) list of company members who may be authorized to hire us for penetration testing:
    - Chief Executive Officer (CEO)
    - Chief Technical Officer (CTO)
    - Chief Information Security Officer (CISO)
    - Chief Security Officer (CSO)
    - Chief Risk Officer (CRO)
    - Chief Information Officer (CIO)
    - VP of Internal Audit	Audit Manager
    - VP or Director of IT/Information Security

## Documents

- This stage also requires the preparation of several documents before a penetration test can be conducted that must be signed by our client and us so that the declaration of consent can also be presented in written form if required.

| Document | Timing for Creation |
| --- | --- |
| 1. Non-Disclosure Agreement (NDA) | After Initial Contact |
| 2. Scoping Questionnaire | Before the Pre-Engagement Meeting |
| 3. Scoping Document | During the Pre-Engagement Meeting |
| 4. Penetration Testing Proposal (Contract/Scope of Work (SoW)) | During the Pre-engagement Meeting |
| 5. Rules of Engagement (RoE) | Before the Kick-Off Meeting |
| 6. Contractors Agreement (Physical Assessments) | Before the Kick-Off Meeting |
| 7. Reports | During and after the conducted Penetration Test |
- Note: Our client may provide a separate scoping document listing in-scope IP addresses/ranges/URLs and any necessary credentials but this information should also be documented as an appendix in the RoE document.
- **Important Note:** These documents should be reviewed and adapted by a lawyer after they have been prepared.

## ****Scoping Questionnaire****

`Scoping Questionnaire` to better understand the services they are seeking.

- **services list:**
    
    
    | ☐ Internal Vulnerability Assessment | ☐ External Vulnerability Assessment |
    | --- | --- |
    | ☐ Internal Penetration Test | ☐ External Penetration Test |
    | ☐ Wireless Security Assessment | ☐ Application Security Assessment |
    | ☐ Physical Security Assessment | ☐ Social Engineering Assessment |
    | ☐ Red Team Assessment | ☐ Web Application Security Assessment |
- Aside from the assessment type, client name, address, and key personnel contact information, some other critical pieces of information include:
    
    
    | How many expected live hosts? |
    | --- |
    | How many IPs/CIDR ranges in scope? |
    | How many Domains/Subdomains are in scope? |
    | How many wireless SSIDs in scope? |
    | How many web/mobile applications? If testing is authenticated, how many roles (standard user, admin, etc.)? |
    | For a phishing assessment, how many users will be targeted? Will the client provide a list, or we will be required to gather this list via OSINT? |
    | If the client is requesting a Physical Assessment, how many locations? If multiple sites are in-scope, are they geographically dispersed? |
    | What is the objective of the Red Team Assessment? Are any activities (such as phishing or physical security attacks) out of scope? |
    | Is a separate Active Directory Security Assessment desired? |
    | Will network testing be conducted from an anonymous user on the network or a standard domain user? |
    | Do we need to bypass Network Access Control (NAC)? |
- Ask about information disclosure and evasiveness:
    - Is the Penetration Test black box (no information provided), grey box (only IP address/CIDR ranges/URLs provided), white box (detailed information provided)
    - Would they like us to test from a non-evasive, hybrid-evasive (start quiet and gradually become "louder" to assess at what level the client's security personnel detect our activities), or fully evasive.

## ****Pre-Engagement Meeting****

Once we have an initial idea of the client's project requirements, we can move on to the `pre-engagement meeting`.

The information we gather during this phase, along with the data collected from the scoping questionnaire, will serve as inputs to the `Penetration Testing Proposal`, also known as the `Contract` or `Scope of Work` (`SoW`).

- **Note**: We may encounter clients during our career that are undergoing their first ever penetration test, or the direct client PoC is not familar with the process. It is not uncommon to use part of the pre-engagement meeting to review the scoping questionnaire either in part or step-by-step.

## ****Contract - Checklist****

| Checkpoint | Description |
| --- | --- |
| ☐ NDA | Non-Disclosure Agreement (NDA) refers to a secrecy contract between the client and the contractor regarding all written or verbal information concerning an order/project. The contractor agrees to treat all confidential information brought to its attention as strictly confidential, even after the order/project is completed. Furthermore, any exceptions to confidentiality, the transferability of rights and obligations, and contractual penalties shall be stipulated in the agreement. The NDA should be signed before the kick-off meeting or at the latest during the meeting before any information is discussed in detail. |
| ☐ Goals | Goals are milestones that must be achieved during the order/project. In this process, goal setting is started with the significant goals and continued with fine-grained and small ones. |
| ☐ Scope | The individual components to be tested are discussed and defined. These may include domains, IP ranges, individual hosts, specific accounts, security systems, etc. Our customers may expect us to find out one or the other point by ourselves. However, the legal basis for testing the individual components has the highest priority here. |
| ☐ Penetration Testing Type | When choosing the type of penetration test, we present the individual options and explain the advantages and disadvantages. Since we already know the goals and scope of our customers, we can and should also make a recommendation on what we advise and justify our recommendation accordingly. Which type is used in the end is the client's decision. |
| ☐ Methodologies | Examples: OSSTMM, OWASP, automated and manual unauthenticated analysis of the internal and external network components, vulnerability assessments of network components and web applications, vulnerability threat vectorization, verification and exploitation, and exploit development to facilitate evasion techniques. |
| ☐ Penetration Testing Locations | External: Remote (via secure VPN) and/or Internal: Internal or Remote (via secure VPN) |
| ☐ Time Estimation | For the time estimation, we need the start and the end date for the penetration test. This gives us a precise time window to perform the test and helps us plan our procedure. It is also vital to explicitly ask how time windows the individual attacks (Exploitation / Post-Exploitation / Lateral Movement) are to be carried out. These can be carried out during or outside regular working hours. When testing outside regular working hours, the focus is more on the security solutions and systems that should withstand our attacks. |
| ☐ Third Parties | For the third parties, it must be determined via which third-party providers our customer obtains services. These can be cloud providers, ISPs, and other hosting providers. Our client must obtain written consent from these providers describing that they agree and are aware that certain parts of their service will be subject to a simulated hacking attack. It is also highly advisable to require the contractor to forward the third-party permission sent to us so that we have actual confirmation that this permission has indeed been obtained. |
| ☐ Evasive Testing | Evasive testing is the test of evading and passing security traffic and security systems in the customer's infrastructure. We look for techniques that allow us to find out information about the internal components and attack them. It depends on whether our contractor wants us to use such techniques or not. |
| ☐ Risks | We must also inform our client about the risks involved in the tests and the possible consequences. Based on the risks and their potential severity, we can then set the limitations together and take certain precautions. |
| ☐ Scope Limitations & Restrictions | It is also essential to determine which servers, workstations, or other network components are essential for the client's proper functioning and its customers. We will have to avoid these and must not influence them any further, as this could lead to critical technical errors that could also affect our client's customers in production. |
| ☐ Information Handling | HIPAA, PCI, HITRUST, FISMA/NIST, etc. |
| ☐ Contact Information | For the contact information, we need to create a list of each person's name, title, job title, e-mail address, phone number, office phone number, and an escalation priority order. |
| ☐ Lines of Communication | It should also be documented which communication channels are used to exchange information between the customer and us. This may involve e-mail correspondence, telephone calls, or personal meetings. |
| ☐ Reporting | Apart from the report's structure, any customer-specific requirements the report should contain are also discussed. In addition, we clarify how the reporting is to take place and whether a presentation of the results is desired. |
| ☐ Payment Terms | Finally, prices and the terms of payment are explained. |

Based on the `Contract Checklist` and the input information shared in scoping, the `Penetration Testing Proposal` (`Contract`) and the associated `Rules of Engagement` (`RoE`) are created.

## ****Rules of Engagement - Checklist****

| Checkpoint | Contents |
| --- | --- |
| ☐ Introduction | Description of this document. |
| ☐ Contractor | Company name, contractor full name, job title. |
| ☐ Penetration Testers | Company name, pentesters full name. |
| ☐ Contact Information | Mailing addresses, e-mail addresses, and phone numbers of all client parties and penetration testers. |
| ☐ Purpose | Description of the purpose for the conducted penetration test. |
| ☐ Goals | Description of the goals that should be achieved with the penetration test. |
| ☐ Scope | All IPs, domain names, URLs, or CIDR ranges. |
| ☐ Lines of Communication | Online conferences or phone calls or face-to-face meetings, or via e-mail. |
| ☐ Time Estimation | Start and end dates. |
| ☐ Time of the Day to Test | Times of the day to test. |
| ☐ Penetration Testing Type | External/Internal Penetration Test/Vulnerability Assessments/Social Engineering. |
| ☐ Penetration Testing Locations | Description of how the connection to the client network is established. |
| ☐ Methodologies | OSSTMM, PTES, OWASP, and others. |
| ☐ Objectives / Flags | Users, specific files, specific information, and others. |
| ☐ Evidence Handling | Encryption, secure protocols |
| ☐ System Backups | Configuration files, databases, and others. |
| ☐ Information Handling | Strong data encryption |
| ☐ Incident Handling and Reporting | Cases for contact, pentest interruptions, type of reports |
| ☐ Status Meetings | Frequency of meetings, dates, times, included parties |
| ☐ Reporting | Type, target readers, focus |
| ☐ Retesting | Start and end dates |
| ☐ Disclaimers and Limitation of Liability | System damage, data loss |
| ☐ Permission to Test | Signed contract, contractors agreement |

## ****Contractors Agreement****

If the penetration test also includes physical testing, then an additional contractor's agreement is required.

This additional `contractor's agreement` is our "`get out of jail free card`" in this case.

## ****Contractors Agreement - Checklist for Physical Assessments****

Checkpoint

- Introduction
- Contractor
- Purpose
- Goal
- Penetration Testers
- Contact Information
- Physical Addresses
- Building Name
- Floors
- Physical Room Identifications
- Physical Components
- Timeline
- Notarization
- Permission to Test

# Information Gathering

![Untitled](3_Penetration%20Testing%20Phases%20-%20Assessment%20Specific%20f4aa5e95b3cd40948deef651c3b0a221/Untitled%201.png)

Once the pre-engagement phase has been completed, and all parties have signed all contractual terms and conditions, the `information gathering` phase begins.

All the steps we take to exploit the vulnerabilities are based on the information we enumerate about our targets.

We can divide them into the following categories:

- Open-Source Intelligence
- Infrastructure Enumeration
- Service Enumeration
- Host Enumeration

## ****Open-Source Intelligence (OSINT)****

OSINT is a process for finding publicly available information on a target company or individuals that allows the identification of events (i.e., public and private meetings), external and internal dependencies, and connections.

## ****Infrastructure Enumeration****

During the infrastructure enumeration, we try to overview the company's position on the internet and intranet. For this, we use OSINT and the first active scans.

In this phase, we also try to determine the company's security measures.

No matter "where" we are positioned, whether we are trying to gain an overview of the infrastructure from the outside (`external`) or examining the infrastructure from the inside (`internal`) of the network.

## ****Service Enumeration****

It is crucial to find out about the service, what `version` it is, what `information` it provides us, and the `reason` it can be used. → `up to date or not`

## ****Host Enumeration****

- Identify which `operating system` is running on the host or server, which `services` it uses, which `versions` of the services, etc.
- Must also identify which `services` it uses for this purpose and on which `ports` they are located.
- Examine the host or server from the inside: look for sensitive `files`, local `services`,  `scripts`,  `applications`, `information`, and other things that could be stored on the host. → also an essential part of the `Post-Exploitation` phase

## ****Pillaging****

- After hitting the `Post-Exploitation` stage, pillaging is performed to collect sensitive information locally on the already exploited host
- information can show the `impact` of a potential attack on our client and be used for further steps to `escalate our privileges` or `move laterally` further in the network.
- Pillaging is explained in other modules separately, where we consider the corresponding steps valuable and necessary.

# Vulnerability Assessment

![Untitled](3_Penetration%20Testing%20Phases%20-%20Assessment%20Specific%20f4aa5e95b3cd40948deef651c3b0a221/Untitled%202.png)

During the `vulnerability assessment` phase, we examine and analyze the information gathered during the information gathering phase.

- An analysis is a detailed examination of an event or process, describing its origin and impact, that with the help of certain precautions and actions, can be triggered to support or prevent future occurrences.

**There are four different types of analysis:**

| Analysis Type | Description |
| --- | --- |
| Descriptive | Descriptive analysis is essential in any data analysis. On the one hand, it describes a data set based on individual characteristics. It helps to detect possible errors in data collection or outliers in the data set. |
| Diagnostic | Diagnostic analysis clarifies conditions' causes, effects, and interactions. Doing so provides insights that are obtained through correlations and interpretation. We must take a backward-looking view, similar to descriptive analysis, with the subtle difference that we try to find reasons for events and developments. |
| Predictive | By evaluating historical and current data, predictive analysis creates a predictive model for future probabilities. Based on the results of descriptive and diagnostic analyses, this method of data analysis makes it possible to identify trends, detect deviations from expected values at an early stage, and predict future occurrences as accurately as possible. |
| Prescriptive | Prescriptive analytics aims to narrow down what actions to take to eliminate or prevent a future problem or trigger a specific activity or process. |

## ****Vulnerability Research and Analysis****

`Information Gathering` and `Vulnerability Research` can be considered a part of descriptive analysis.

In `Vulnerability Research`, we look for known vulnerabilities, exploits, and security holes that have already been discovered and reported.

[Common Vulnerabilities and Exposures (CVE)](https://www.cve.org/ResourcesSupport/FAQs)

- We can find vulnerability disclosures for each component using many different sources. These include, but are not limited to:
    
    
    | https://www.cvedetails.com/ | https://www.exploit-db.com/ | https://www.securityfocus.com/vulnerabilities |
    | --- | --- | --- |
    | https://packetstormsecurity.com/ | https://nvd.nist.gov/vuln/search?execution=e2s1 | https://vulners.com/ |

This is where `Diagnostic Analysis` and `Predictive Analysis` is used.

## ****Assessment of Possible Attack Vectors****

`Vulnerability Assessment` also includes the actual testing, which is part of `Predictive Analysis`. In doing so, we analyze historical information and combine it with the current information that we have been able to find out.

## ****The Return****

Suppose we are unable to detect or identify potential vulnerabilities from our analysis. In that case, we will return to the `Information Gathering` stage and look for more in-depth information than we have gathered so far.

# Exploitation

![Untitled](3_Penetration%20Testing%20Phases%20-%20Assessment%20Specific%20f4aa5e95b3cd40948deef651c3b0a221/Untitled%203.png)

During the `Exploitation` stage, we look for ways that these weaknesses can be adapted to our use case to obtain the desired role (i.e., a foothold, escalated privileges, etc.).

## ****Prioritization of Possible Attacks****

Which of those attacks we prioritize higher than the others depends on the following factors:

- **Probability of Success**
    
    [CVSS Scoring](https://nvd.nist.gov/vuln-metrics/cvss) can help us here, using the [NVD calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) better to calculate the specific attacks and their probability of success.
    
- **Complexity**
    
    The effort of exploiting a specific vulnerability. Estimate how much time, effort, and research is required to execute the attack on the system successfully.
    
- **Probability of Damage**
    
    Estimating the `probability of damage` caused by the execution of an exploit plays a critical role, as we must avoid any damage to the target systems.
    

### ****Prioritization Example****

| Factor | Points | Remote File Inclusion | Buffer Overflow |
| --- | --- | --- | --- |
| 1. Probability of Success | 10 | 10 | 8 |
| 2. Complexity - Easy | 5 | 4 | 0 |
| 3. Complexity - Medium | 3 | 0 | 3 |
| 4. Complexity - Hard | 1 | 0 | 0 |
| 5. Probability of Damage | -5 | 0 | -5 |
| Summary | max. 15 | 14 | 6 |

we would prefer the `remote file inclusion` attack. It is easy to prepare and execute and should not cause any damage if approached carefully.

## ****Preparation for the Attack****

In situations where high-quality, known working PoC exploit code cannot be found, it may be necessary to reconstruct the exploit locally on a VM representing the target host to figure out what needs to be adapted and changed. In other situations, if we encounter misconfigurations or vulnerabilities that we see often, it may be possible to use a known tool or exploit. If we are ever in doubt before running an attack, it's always best to check with the client. If the client opts for us not to proceed with exploitation, we can note in the report that it was not confirmed actively but is likely an issue that needs to be addressed. During penetration tests, we should always use our best judgment if a particular attack seems too risky or could potentially cause a disruption. Once we have successfully exploited a target and have initial access, we'll move on to the post-exploitation and lateral movement stages.

# Post-Exploitation

![Untitled](3_Penetration%20Testing%20Phases%20-%20Assessment%20Specific%20f4aa5e95b3cd40948deef651c3b0a221/Untitled%204.png)

Assume we successfully exploited → We must again consider whether or not to utilize `Evasive Testing` in the `Post-Exploitation` stage.

The `Post-Exploitation` stage aims to obtain sensitive and security-relevant information from a local perspective and business-relevant information that, in most cases, requires higher privileges than a standard user.

Includes the following components:

| Evasive Testing | Information Gathering |
| --- | --- |
| Pillaging | Vulnerability Assessment |
| Privilege Escalation | Persistence |
| Data Exfiltration |  |

## ****Evasive Testing****

If detected, we may lose access to the network or a host, and threat hunting may begin. However, we can still provide value by identifying gaps in monitoring and processes and writing up an attack chain. We can also improve our evasion skills by studying how and why we were detected.

Evasive testing is divided into three different categories:

| Evasive | Hybrid Evasive | Non-Evasive |
| --- | --- | --- |

Three types of evasive testing can be used in combination: Non-evasive, Hybrid-evasive, and Evasive. Non-evasive testing is used when security measures around the network may limit or stop the test. Hybrid-evasive testing is used to test specific components and security measures defined in advance. Evasive testing is used to evade and pass security traffic and systems in the customer's infrastructure.

## ****Information Gathering****

In Post-Exploitation, we need to gather new information about the system and network from an internal perspective. This involves repeating Information Gathering and Vulnerability Assessment stages.

## ****Pillaging****

Pillaging is the stage where we examine the role of the host in the corporate network. We analyze the network configurations, including but not limited to:

| Interfaces | Routing | DNS |
| --- | --- | --- |
| ARP | Services | VPN |
| IP Subnets | Shares | Network Traffic |

`Understanding the role of the system` we are on also gives us an excellent understanding of how it communicates with other network devices and its purpose.

## ****Persistence****

After getting an overview of the system, the immediate next step is to maintain access to the exploited host. This is crucial and is often used as the first step before the `Information Gathering` and `Pillaging` stages. It's important to work flexibly during this phase and adapt to the circumstances as each system is individually configured by a unique administrator. For instance, if a buffer overflow attack on a service may crash it, establishing persistence to the system as soon as feasible can avoid attacking the service multiple times and potentially disrupting it. Losing the connection may result in not being able to access the system similarly.

## ****Vulnerability Assessment****

After gaining access to the system, we repeat the Vulnerability Assessment stage from inside the system. We prioritize the information and aim to escalate privileges if necessary. We distinguish between harmful exploits and non-disruptive attacks and consider the previous Vulnerability Assessment stage.

## ****Privilege Escalation****

Privilege escalation is crucial for gaining the highest possible privileges on a system or domain, such as `root` access on `Linux-based` systems or `administrator` access on `Windows-based` systems. This enables moving through the entire network without restriction. Stored credentials from higher-privileged users obtained during information gathering can also be used for privilege escalation.

## ****Data Exfiltration****

During `Information Gathering` and `Pillaging`, we may find personal information and customer data. Some clients may want to test if it's possible to exfiltrate such data. Security measures such as Data Loss Prevention`DLP` and Endpoint Detection and Response `EDR` help detect and prevent data exfiltration. Before transferring any actual data, we should check with the customer and create fake data to test protection mechanisms.

Companies must adhere to data security regulations depending on the type of data involved. These include, but are not limited to:

| Type of Information | Security Regulation |
| --- | --- |
| Credit Card Account Information | Payment Card Industry (PCI) |
| Electronic Patient Health Information | Health Insurance Portability and Accountability Act (HIPAA) |
| Consumers Private Banking Information | Gramm-Leach-Bliley (GLBA) |
| Government Information | Federal Information Security Management Act of 2002 (FISMA) |

Some frameworks companies may follow include:

| (NIST) - National Institute of Standards and Technology | (CIS Controls) - Center for Internet Security Controls |
| --- | --- |
| (ISO) - International Organization for Standardization | (PCI-DSS) - The Payment Card Industry Data Security Standard |
| (GDPR) - General Data Protection Regulation | (COBIT) - Control Objectives for Information and Related Technologies |
| (FedRAMP) - The Federal Risk and Authorization Management Program | (ITAR) - International Traffic in Arms Regulations |
| (AICPA) - American Institute of Certified Public Accountants | (NERC CIP Standards) - NERC Critical Infrastructure Protection Standards |

# Lateral Movement

![Untitled](3_Penetration%20Testing%20Phases%20-%20Assessment%20Specific%20f4aa5e95b3cd40948deef651c3b0a221/Untitled%205.png)

During the Lateral Movement stage, we test what an attacker could do within the entire network. The goal is to get sensitive data or find all ways that an attacker could render the network unusable. [Ransomware](https://www.csoonline.com/article/563507/what-is-ransomware-how-it-works-and-how-to-remove-it.html) is a common example that can spread across the entire network and lock down all systems, making them unusable until a decryption key is entered.

In this stage, we'll manually test how far we can move in the network and identify exploitable vulnerabilities from an internal perspective. We'll go through several phases to accomplish this:

1. Pivoting
2. Evasive Testing
3. Information Gathering
4. Vulnerability Assessment
5. (Privilege) Exploitation
6. Post-Exploitation

As seen in the graphic above, we can move to this stage from the `Exploitation` and the `Post-Exploitation` stage. Sometimes we may not find a direct way to escalate our privileges on the target system itself, but we have ways to move around the network. This is where `Lateral Movement` comes into play.

## ****Pivoting****

- Most systems do not have the tools required to efficiently enumerate an internal network, so techniques like pivoting are used to use the exploited host as a proxy to perform scans from the attack machine and route network requests to the internal network.
- `Pivoting`, also known as `tunnelling`, allows for penetration of non-routable networks that are not publicly reachable, providing access to inaccessible systems via an intermediary system.

## ****Evasive Testing****

Consider evasive testing at the Lateral Movement stage. Different tactics have different procedures to avoid triggering alarms. Protect against lateral movement with network `segmentation`, `threat monitoring`, `IPS/IDS`, `EDR`, etc. Understand how they work to bypass them efficiently and apply strategies to avoid detection.

## ****Information Gathering****

Before targeting the internal network, we need to know which systems are reachable from our system. This information may already be available from the last post-exploitation stage. We return to the Information Gathering stage, but this time, from inside the network. Once we have discovered all hosts and servers, we can enumerate them individually.

## ****Vulnerability Assessment****

Vulnerability assessment inside a network differs from previous procedures since errors happen more often in this environment. `Groups` and user `rights` play a crucial role, and users commonly share information and documents. This information is valuable when planning attacks, as compromising a user account assigned to a particular group may provide access to crucial internal information, identifying flaws and furthering access.

## ****(Privilege) Exploitation****

During the Lateral Movement stage, we explore and prioritize paths to access other systems. We may crack passwords and hashes, use existing credentials, or intercept hashes with tools like Responder. The goal is to move through the internal network using existing data in versatile ways.

## ****Post-Exploitation****

After accessing a host or server, we repeat the post-exploitation stage to collect system and business information. We must handle sensitive data according to the contract's rules. Then, we move to the Proof-of-Concept phase to demonstrate our findings and help with remediation.