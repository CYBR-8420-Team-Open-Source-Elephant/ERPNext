# ERPNext
[Source Repository](https://github.com/frappe/erpnext)

# Description

## Overview

ERPNext is an enterprise resource planning application that supports a variety of features necessary to operate and grow a business. The software is available for implementation amongst large businesses, small teams and freelancers. It offers a range of operational activities such as tracking inventory, managing finances, and organizing projects within a single product offering. Customers have a low/no code interface that gives them freedom to customize and tailor the software to their business needs. While the software is free and open-source, users are charged for hosting through Frappe Cloud.

## Contributors & Activity

Following a review of ERPNext’s analytics on GitHub, the software holds more than 28,000 GitHub Stars. In the last 30 days, ERPNext has seen 13-14 contributors, alongside moderate activity with 19 new issues posted in the past week. Recent issues mainly include bug and feature requests. Updates seem to be frequent with 5 in the last month and 1,602 across the life of the project.

## Use & Popularity

ERPNext is currently ranked in the Top 10 ERP Systems for 2025 by Software Connect on Linkedin. Per their website, the software spans multiple industries and has been adopted by more than 30,000 companies through partners in over 30 countries. Companies include brands like Chewy, Tanteo Spirits, and Newmatik - a user transitioned from Microsoft Navision. 

## Languages Used & Platform

ERPNext’s framework is written in Python and Javascript. The software runs on the Frappe Framework, a framework built for ERPNext,  which is a full-stack web application with a Vue-based UI library.

## Documentation Sources

Please see the links below for documentation and additional resources provided by ERPNext for users and developers.

[Documentation](https://docs.frappe.io/erpnext/user/manual/en/introduction) - Official Documentation Link  
[Frappe School](https://school.frappe.io/lms/courses) - Various courses created by to teach about ERPNext and Frappe Framework  
[Forum](https://discuss.frappe.io/c/erpnext/6) - Link for engagement with users and service providers

# Hypothetical Operational Environment

A hospital uses ERPNext to manage finance, HR, patient billing, inventory, lab requests, and maintenance requests. ERPNext also integrates with other systems such as the Electronic Health Record System, Disaster Recovery, and MFA. Many hospital devices are also integrated including equipment and medical imaging devices. ERPNext allows this management while supporting different roles within the hospital system including doctors, nurses, lab staff, management, and receptionist/billing. These users expect various security functionalities from the software. Some of these functionalities include SSO (single sign-on), MFA ( multi-factor authentication), audit logging, password protection, disaster recovery/backups, regulatory compliance, and role based permissions. 

Threats perceived by users of ERPNext in the hospital setting could include unauthorized access to privileged information (patient or employee, ransomware attacks, password theft, and data breaches).

Security features to combat these threats that are provided by the software include user authentication, login controls, password security (hashing, strength requirements), role-based access control, audit logging, and encryption of data in rest/transit.

![Systems Engineering Diagram](/systems-engineering-diagram.png)

# Team Motivation

For our motivation, we were looking for a program that was impactful to people, as well as a diversified and well connected program. We settled on ERPNext for a variety of reasons. There were a few different aspects that were discussed during our initial meeting with the instructor, such as user authentication, data sensitivity, role management, and complexity of environment. This software deals with a variety of different systems, from accounting to asset management. Naturally this will require user authentication as well as separation of roles. The software also brags a collection of tools normally separated, providing a full suite of tools for a small business, thus complex. As this deals with a wide variety of data, it also deals with different kinds of sensitive data.
Beyond software specifications matching what is needed, the software is written mostly in a comfortable language for the team, python. Allows for an interesting software to analyze, and a wide spread of different systems we can look into. It appears as a suitable project not only for project specifications but also for team curiosity. 


# License

ERPNext uses the Gnu General Public License version 3 (GPL v3). GPL v3 is a “copyleft” license. It allows the code to be used and distributed for commercial or non-commercial purposes. It also allows for modifications to the code. Unlike permissive open source licenses, GPL v3 requires that any distributions or modifications of the code are also licensed under GPL v3 ([source](https://fossa.com/blog/open-source-software-licenses-101-gpl-v3/)).

# Procedure for Contributing

The [constributing guidelines](https://github.com/frappe/erpnext?tab=contributing-ov-file) for ERPNext include rules to ensure a positive experience for developers. They require that issues focus on a single topic rather than lumping multiple issues together and include a brief, descriptive explanation. Bug reports must include clear steps to reproduce the problem, as well as the version number for the software and a clear title. Feature requests must specify the desired behavior. They should identify how the solution might look, possibly by including mockups. Before submitting any change request, contributors must check that no one else has already raised the issue before.

Frappe also has a separate [policy](https://frappe.io/security) for reporting security vulnerabilities. Vulnerability reports must include contact information for the reporter, a reference or advisory number, a description of the vulnerability, technical details describing how the vulnerability could be exploited, and disclosure plans. Frappe requests 10-15 days to respond to issues. If the issue is not addressed within 3 months, they request that the contributor contacts them via email at security@frappe.io.

ERPNext includes a code of conduct that is adapted from the [Contributor Covenant](https://www.contributor-covenant.org/), which is a widely used open source code of conduct. It requires respectful communication among contributors and prohibits harassment or discrimination. The project maintainers reserve the right to edit or remove any communications or commits that violate the code of conduct. They also reserve the right to temporarily or permanently ban a contributor. Unacceptable behavior can be confidentially reported to the maintainers via email at hello@frappe.io.

# Security-Related History of ERPNext

ERPNext has previously experienced several security issues that mainly stem from its flexibility and large attack surface. Early versions were vulnerable to SQL injection attacks, where authenticated users could manipulate queries. Later releases saw multiple cross-site scripting (XSS) issues, such as CVE-2022-28598, which allowed malicious scripts to be injected into web pages. More recently, in 2025, a cross-site request forgery (CSRF) flaw was disclosed, enabling attackers to perform unauthorized actions like password resets.

A Server-Side Request Forgery in 2022 was found that could lead to account takeover. A remote code execution exploit in version 13.4.0 (2023) through ERPNext’s “server script” feature, where sandbox restrictions could be bypassed. These vulnerabilities highlight the challenges of balancing ERPNext’s framework with strong security controls.

In response, the ERPNext community has improved input sanitization, access controls, CSRF protections, and security patch releases. The project now has a public security policy where you can report security issues detected, and the community helps resolve them. Running the most up-to-date version is key to being safe while using this software. 

# Reflection

In our initial search for topics, we focused on security tools. However, we found many of those projects to be to narrow in scope. We then pivoted to projects with security requirements and a need for assurance rather than projects that can be used to fulfill security requirements. We each researched potential projects and found at least one that we felt would make a good topic. From that list of topics, we decided that ERPNext fit the requirements for the assignemnt and used languages and technologies that all members of the group had familiarity with. While completing this assignment, we researched how open-source projects fulfill security requirements over time and learned about how major open-source projects operate. We found boards on GitHub to be a useful tool to collaborate and track work. We also found Discord to be useful for communication.