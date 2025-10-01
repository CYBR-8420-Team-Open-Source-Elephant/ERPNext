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

Actors: Production Manager, Insider with Excess Privileges (Disgruntled Operator), Inital-Access Broker

Use Case: The Production Manager uses ERPNext to create and adjust capacity plans for manufacturing. Suppliers interact with ERPNext through subcontracting orders by receiving raw materials, performing outsourced operations, and returning finished goods. The Production Manager can allocate resources and update schedules to keep production on track. All adjustments to capacity plans and subcontracting orders are logged for accountability, and approval workflows require managerial review for high-impact changes. Supplier inputs are validated against expected schemas and authenticated through API tokens to prevent errors or unauthorized updates.

Misuse Case: An insider with excessive privileges may attempt to manipulate capacity planning data to hide delays or falsify workloads. External suppliers may attempt to inject invalid data or tamper with subcontracting receipts. These actions are mitigated by role-based access controls that limit who can create or publish capacity plans, and by approval workflows that require a second review for significant changes. Audit logging records every change for detection and response. On the subcontracting side, supplier data is safeguarded with API authentication, schema validation, and alerts that flag abnormal consumption or receipt patterns. Together these countermeasures ensure misuse attempts are detected, blocked, or escalated for additional authorization.derived from our analysis.

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