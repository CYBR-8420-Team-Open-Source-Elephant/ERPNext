# Requirements for Software Security Engineering

## Use/Misuse Cases

### Use/Misuse Case: Accounting

Add diagram here

#### Description


### Use/Misuse Case: Order Management

Add diagram here

#### Description


### Use/Misuse Case: Manufacturing

![Use/Misuse Case Manufacturing Photo](/Use_Misuse%20Case%20-%20Manufacturing.png)

#### Description

In this use case the Production Manager interacts with ERPNext to create and adjust capacity plans. Suppliers interact through subcontracting orders and misusers include insiders with excessive privileges who may try to manipulate scheduling to hide delays or falsify workloads. External suppliers may attempt to inject invalid data or tamper with subcontracting receipts. Countermeasures include role-based access controls to restrict who can publish or modify plans. Approval workflows require a second review for major changes. Audit logging captures every adjustment for accountability and on the subcontracting side supplier inputs are safeguarded through API authentication, schema validation and alerts that flag unusual consumption or receipt patterns. These controls ensure that misuse attempts are detected, blocked or require additional authorization. They align ERPNext’s functionality with the security requirements derived from our analysis.

### Use/Misuse Case: Asset Management

Add diagram here

#### Description


### Use/Misuse Case: Projects

Add diagram here

#### Description


## AI for Use/Misuse Cases


## Security Requirements

### Requirement Name

Brief description of the requriement

#### Assessment

Explain whether the features of ERPNext fulfill this requirement. Include link to the documentation if applicable.


## Project Documentation Review

The ERPNext documentation provides solid coverage of core security features such as role-based access control, user and permission management, workflows for approvals, and auditability through versioning and audit trails. The installation instructions are straightforward, and the documentation website is easy to follow, but we noticed that some links (like those on the “Users” page) are out of date. A major area for improvement is the way security guidance is presented!! Information on topics such as RBAC, password policies, and logging is scattered across different sections rather than consolidated in one place. The documentation would benefit from a dedicated “Security Hardening” section that pulls together step-by-step guides, checklists, and configuration templates. Security details around areas like input validation, DDoS protection, and system/database hardening could be expanded. In our opinion having clearly accessible documentation contributions via GitHub could lower the barrier for community input.

## Reflection