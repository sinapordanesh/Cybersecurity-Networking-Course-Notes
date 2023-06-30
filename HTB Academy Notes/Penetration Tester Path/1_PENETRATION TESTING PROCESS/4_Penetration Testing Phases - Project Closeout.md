# 4_Penetration Testing Phases - Project Closeout

# Proof-of-Concept

![Untitled](4_Penetration%20Testing%20Phases%20-%20Project%20Closeout%2073223c6500424ead9d394e74a7ff9edb/Untitled.png)

Proof of Concept (PoC) or Proof of Principle is a project management term that serves as a feasibility study for a project. It helps to determine whether a project is technically and financially viable. In our case, it helps to confirm the discovered vulnerabilities and identify and minimize risks. It serves as a basis for further work and decision-making and enables the necessary steps to secure the corporate network.

- Proof of Concept (PoC) is often integrated into the development process for new application software or IT security solutions.
- PoC is used to prove vulnerabilities in operating systems or application software.
- It helps developers or administrators validate, reproduce, see the impact, and test their remediation efforts.
- PoC can have different representations, including documentation or a script/code that automatically exploits the vulnerabilities found.
- Administrators and developers can modify and secure the systems so that the script we created no longer works, but this does not mean that the information obtained from the script cannot be obtained in another way.
- The report should help them see the entire picture, focus on the broader issues, and provide clear remediation advice.
- Including an attack chain walkthrough in the event of domain compromise during an internal is a great way to show how multiple flaws can be combined.
- Fixing one flaw will break the chain, but the other flaws will still exist. It's important to fix all the flaws.
- A weak password is an underlying vulnerability, and the `password policy` is the problem.
- Administrators and developers are responsible for the functionality and quality of their systems and applications.
- High quality stands for high standards, which we should emphasize through our remediation recommendations.

# Post-Engagement

![Untitled](4_Penetration%20Testing%20Phases%20-%20Project%20Closeout%2073223c6500424ead9d394e74a7ff9edb/Untitled%201.png)

After an engagement is complete, there are many activities that must be performed to close out the engagement fully. These activities may differ slightly depending on the engagement, but they are generally contractually binding and must be performed to ensure that the engagement is properly concluded.

## ****Cleanup****

After completing testing, we should perform the necessary cleanup, including deleting tools/scripts and reverting any minor configuration changes. Detailed notes of all activities should be kept to make cleanup easy and efficient. If we can't access a system to delete an artifact or revert a change, we should notify the client and document the issues in the report appendices. Any changes made should be documented in the report appendices in case the client receives alerts and needs to confirm our testing.

## ****Documentation and Reporting****

When completing the engagement, we must document all findings for the report, including command output, screenshots, affected hosts, and any relevant information. We must also retrieve all scan and log output. We should not retain sensitive data.

Our report deliverable should consist of the following:

- Attack chain detailing steps taken to achieve compromise
- Executive summary for non-technical audience
- Detailed findings with risk rating, impact, remediation recommendations, and references
- Steps to reproduce each finding for remediation team
- Near, medium, and long-term recommendations
- Appendices including target scope, OSINT data, password cracking analysis, discovered ports/services, compromised hosts/accounts, files transferred, AD security analysis, relevant scan data/documentation, and other relevant information

## ****Report Review Meeting****

A report review meeting is held after the draft report is delivered. Attendees include the same people from the client and the firm performing the assessment. Each finding is briefly explained from a personal perspective, with a focus on high-risk findings. The entire report is not read word for word during the meeting.

## ****Deliverable Acceptance****

The Scope of Work should define deliverable acceptance. In penetration test assessments, we deliver a report marked `DRAFT` and give the client a chance to review and comment. Once the client has submitted feedback, we issue them a new version of the report marked `FINAL`. Some audit firms may not accept a report with a `DRAFT` designation, so keeping a uniform approach across all customers is best.

## ****Post-Remediation Testing****

We review documentation provided by the client showing evidence of remediation or a list of remediated findings. We reaccess the target environment and test each issue to ensure it was appropriately remediated. We issue a post-remediation report that clearly shows the state of the environment before and after post-remediation testing.

For example, we may include a table such as:

| # | Finding Severity | Finding Title | Status |
| --- | --- | --- | --- |
| 1 | High | SQL Injection | Remediated |
| 2 | High | Broken Authentication | Remediated |
| 3 | High | Unrestricted File Upload | Remediated |
| 4 | High | Inadequate Web and Egress Filtering | Not Remediated |
| 5 | Medium | SMB Signing Not Enabled | Not Remediated |
| 6 | Low | Directory Listing Enabled | Not Remediated |

We need to show proof that the issue is resolved through scan output or failure of original exploitation techniques.

## ****Role of the Pentester in Remediation****

As third-party auditors, we should not perform remediation during a penetration test. We can give general remediation advice and explain findings, but we should not implement changes or give precise remediation advice. This helps maintain the assessment's integrity and avoids potential conflicts of interest.

## ****Data Retention****

After a penetration test, data retention and destruction requirements vary depending on country and firm policies. These should be outlined in the contract language of the Scope of Work and the Rules of Engagement, following [Penetration Testing Guidance](https://www.pcisecuritystandards.org/documents/Penetration_Testing_Guidance_March_2015.pdf) from the PCI Data Security Standard (PCI DSS):

[Penetration_Testing_Guidance_March_2015.pdf](4_Penetration%20Testing%20Phases%20-%20Project%20Closeout%2073223c6500424ead9d394e74a7ff9edb/Penetration_Testing_Guidance_March_2015.pdf)

- It's recommended that the tester retains evidence collected during the engagement following best practices and considering any laws that must be followed for the retention of evidence. There are no specific PCI DSS requirements regarding the retention of evidence, but it should be available upon request from authorized entities.

## ****Close Out****

After delivering the final report, assisting the client with questions regarding remediation, and performing post-remediation testing/issuing a new report, the project can be closed out. We should ensure that any systems used to connect to the client's systems or process data have been wiped or destroyed, and any leftover artifacts are stored securely. The final steps would be invoicing the client, collecting payment, and following up with a post-assessment client satisfaction survey. Discussions for follow-on work may arise if the client was pleased with our work and day-to-day interactions.

As we continually grow our technical skillset, we should always look for ways to improve our soft skills and become more well-rounded professional consultants. In the end, the `client will usually remember interactions` during the assessment, communication, and how they were treated/valued by the firm they engage, `not the fancy exploit chain the pentester pulled off to pwn their systems`. Take this time to self-reflect and work on continuous improvement in all aspects of your role as a professional penetration tester.