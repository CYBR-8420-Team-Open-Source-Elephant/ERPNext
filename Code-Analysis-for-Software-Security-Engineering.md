# Code Analysis for Software Security Engineering

[Project Board](https://github.com/orgs/CYBR-8420-Team-Open-Source-Elephant/projects/3/views/1)


----

## Part 1: Code Review


----


## Code Review Strategy 
The software we evaluated is ERPNext, built on the Frappe framework. Because the codebase is very large and heavily framework-driven, our strategy was:

* Scenario/weakness-based manual review of modules tied to our misuse cases and assurance claims (RBAC, authentication, logging, manufacturing workflows, financial logic).

* Automated scanning with SonarQube/SonarCloud on the develop branch, then manual triage of the most relevant findings.

The biggest challenges were the size of the codebase, the amount of implicit Frappe behavior, and distinguishing real security issues from framework conventions or test data. We addressed this by scoping to a small set of high-risk files, using SonarQube to point us at suspicious lines, and then using documentation to verify if each SonarQube alert was true.

----

## Selected CWEs
We organized our review around the following CWEs, which we considered most relevant for ERPNext in our threat model:

CWE-272 – Least Privilege Violation

CWE-266 – Incorrect Privilege Assignment

CWE-284 – Improper Access Control

CWE-732 – Incorrect Assignment for Critical Resource

CWE-603 – Use of Client-Side Authentication

CWE-425 – Direct Request (“Forced Browsing”)

CWE-89 – Improper Neutralization of Special Elements used in an SQL Command (SQL Injection)

CWE-778 – Insufficient Logging

CWE-307 – Improper Restriction of Excessive Authentication Attempts

CWE-552 – Files or Directories Accessible to External Parties

CWE-20 – Improper Input Validation

CWE-200 – Exposure of Sensitive Information to an Unauthorized Actor

CWE-319 – Cleartext Transmission of Sensitive Information

CWE-570 – Expression is Always False

CWE-561 – Dead Code


----

## Part 2: Key Findings and Contributions

----

## Manual Code Review

----

## Other Reviewed Findings

----

## Automated Code Review

----

## Team Reflection



