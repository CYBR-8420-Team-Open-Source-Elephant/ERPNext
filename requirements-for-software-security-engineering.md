# Requirements for Software Security Engineering

## Use/Misuse Cases

### Use/Misuse Case: Accounting

Add diagram here

#### Description


### Use/Misuse Case #2: Order Management

![Use_Misuse Case - Order Management](/Use_Misuse%20Case%20-%20Order%20Management.drawio.drawio.png)

Actors:
DieNet Hacktivist Group and Sales Supervisor

Use Case:

The sales supervisor approves submitted sale orders.

Misuse Case:

An external hacktivist group, DieNet, launches a joint DDOS/malware deployment attack. This will flood the system with orders in an attempt to disrupt services and deploy harmful malware to move laterally through the system.

ERPnext provides many built-protections against a potential DDoS/malware attack based on the above use/misuse case. Some of these include basic rate limiting, role-based permission features, IP restricting, and audit logging. These security features help mitigate the misuse case. However, the documentation regarding DDoS attacks or sophisticated malware deployment seems to be lacking from OSS documentation and the codebase. The IP restrictions are also not decently hardened, leaving space for improvement. Additional guidance, playbooks, and standards would be beneficial in improving mitigations/security requirements for this misuse case. Overall, existing security features align well with requirements but should be enhanced to further strengthen security. 

### Use/Misuse Case: Manufacturing

Add diagram here

#### Description

### Use/Misuse Case #4: Asset Management

![Asset Management Use Case](/use-case-asset-management.png)

Actors: Asset manager, Rogue Employee, and System Administrator

Use Case: The asset manager uses ERPNext's asset reports to keep track of the value of assets held by the company. The system administrator manages the deployment of ERPNext and keeps it secure by monitoring for suspicious activity and modifying user permissions when necessary.

Misuse Case: A rogue employee wants to take revenge on the company by leaking sensitive financial information. When his account permissions are revoked due to suspicious activity, he pivots to attempting to steal the account of another user, and is thwarted by password requirements designed to prevent brute-force attacks and multi-factor authentication.


### Use/Misuse Case #5: Projects

![Projects Use Case](/use-case-projects.png)

Actors: Customer, Project Manager, Embezzler, and System Administrator

Use Case: A customer receives a sales invoice generated from the project management and time tracking features of ERPNext. The project manager is in charge of the project that serves this customer. He uses ERPNext to track how he spent his time on the project and to approve the timesheets of the employees that he manages. The system administrator views project logs to look for suspicious user behavior. If any suspicious behavior is found, the administrator can temporarily or permanently restrict the permissions of a user. The administrator is also part of an approval workflow for managing logs and must approve any requests to delete logs.

Misuse Case: A dishonest employee wants to embezzle money from the company and its customers. He attempts to create falsified timesheets, but these are caught by the project manager, who must approve timesheets for this project. The embezzler then attempts to edit past timesheets. This is outside the permissions of the embezzler's user type, and is tracked by projects logs for the system administrator to see. He also tries to create fake sales invoices, but this is again tracked in the project logs for the system administrator to see. Out of fear of being caught, the embezzler tries to delete the logs that show his malicious behavior. This is again outside of his permissions, and performing such an action requires the approval of a system administrator.


## AI for Use/Misuse Cases


## Security Requirements

### Role-Based Access Control

Deployments of ERPNext should follow the principle of least privilege. Users should only be able to create, read, update, and delete data as is necessary for their role. Permissions should be restricted by default.

#### Assessment

ERPNext has a role-based permissions system ([source](https://docs.frappe.io/erpnext/user/manual/en/role-based-permissions)). A wide range of actions can be allowed or disallowed for a role on different document types. Permissions can also be added for a specific individual user ([source](https://docs.frappe.io/erpnext/user/manual/en/user-permissions)). There is an optional "Strict Permissions" setting that will cause any undefined permissions to be considered disabled unless they are specifically granted to a user ([source](https://docs.frappe.io/erpnext/user/manual/en/user-permissions#23-strict-permissions)).


### Approval Workflows

Users of ERPNext should be able to create approval workflows in which certain actions require the approval of specific users. This can mitigate the damage that an insider threat can cause by performing sensitive actions.

#### Assessment

Custom workflows are supported by ERPNext ([source](https://docs.frappe.io/erpnext/user/manual/en/workflows)). Workflows can require the approval of users in particular roles. Approvals can be required if certain conditions are met. For example, a manager may need to approve a sales invoice with a charge that is over a certain value.


### Input Validation and Business Rule Checks

User inputs in the ERPNext UI should be sanitized and validated to prevent against attacks such as SQL injection. ERPNext should also be able to check inputs against business rules, potential requiring the approval of a member of a user group if values exceed certain quantities.

#### Assessment

The Frappe framework supports input field validation ([source](https://docs.frappe.io/framework/user/en/basics/doctypes/fieldtypes)). ERPNext also validates values based on business rules. One example of this is in [Capacity Planning based on Work Order](https://docs.frappe.io/erpnext/user/manual/en/capacity-planning). Further validation can be implemented through the previously discussed approval workflow feature. While extensive testing would be necessary to fully assess ERPNext's input validation, analysis of the documentation relating to key interactions indicates that this requirement is addressed.


### Audit Logs

ERPNext should log the actions of users. There should be a clear audit log so that suspicous user activity can be detected. The history of edits to data in ERPNext shold be tracked so that content can be restored after accidental or malicous edits or deletions.

#### Assessment

ERPNext features an access log that tracks when data is exported by users ([source](https://docs.frappe.io/erpnext/user/manual/en/access-log)). ERPNext also features optional document versioning which tracks the history of edits to a document ([source](https://docs.frappe.io/erpnext/user/manual/en/document-versioning)). These features partially fulfill the requirement, but they could be further expanded. The access logs could track more user actions, such as creating, editing, or deleting data. There could also be an automated warning system that detects suspicious user activity. For example, a notification could be sent to an administrator if a user makes a high number of edits in a short amount of time. These additions to logging could help detect, prevent, or mitigate the actions of malicious users.


### API Authentication

Any sensitive REST APIs for ERPNext should require authentication.

#### Assessment

The Frappe framework allows REST API authentication through tokens or passwords and supports OAuth 2.0 ([source](https://docs.frappe.io/framework/user/en/api/rest)). Further code analysis and extensive testing is necessary to determine the effectiveness of its implementation in ERPNext.

### Password Requirements

ERPNext should require users to use strong passwords to prevent brute-force password attacks.

#### Assessment

ERPNext has a password strength checker ([source](https://docs.frappe.io/erpnext/user/manual/en/system-settings#18-password)). Administrators can set a minimum password strength score. While this feature does support the security requirement, it could be improved with further customization options. Administrators may wish to set specific length requirements or require certain character types rather than relying on the strength checker that ERPNext provides.


### Account Lockout Policy

Repeated failed login attempts should cause a user to be locked out of their account to prevent brute-force password attacks.

#### Assessment

ERPNext can be configured to lock an account for a certain amount of time after a number of failed login attempts is reached ([source](https://docs.frappe.io/erpnext/user/manual/en/system-settings#16-brute-force-security)). This feature could be expanded to further harden password security. A cascading lockout time that increases as failed attempts increase could further aid in preventing brute-force attacks. Accounts could also be permanently locked until unlocked by a privileged user if a certain number of failed login attempts is met.


### Rate Limiting

ERPNext should be able to limit network requests in order to prevent denial-of service-requests.

#### Assessment

The Frappe framework supports rate limiting ([source](https://docs.frappe.io/framework/user/en/rate-limiting)). Requests over a set limit can be ignored and will result in a an HTTP 429 "Too Many Requests" response. Further code analysis and extensive testing is necessary to determine the effectiveness of its implementation.


### IP Restriction

ERPNext should be able to restrict users from logging in to the system from outside of specific IP addresses. This can make it more difficult for outside threats to access the system and helps to prevent denial-of-service attacks.

#### Assessment

ERPNext can be configured to block logins from outside of a whitelist of IP addresses ([source](https://docs.frappe.io/erpnext/user/manual/en/adding-users#28-security-settings)). It can also be configured to require multi-factor authentication when logging in from outside of the whitelisted IP addresses ([source](https://docs.frappe.io/erpnext/user/manual/en/system-settings#17-two-factor-authentication)).


## Project Documentation Review


## Reflection
Across the individual reflections, a common theme included the value that the use/misuse diagrams provided throughout the assignment process. These allowed for the team to visualize and trace the interactions occurring between the actors and software. These interactions included threat use/misuse cases that the software could potentially interact with in the real world. These visualizations also allowed us to better identify the security requirements that are needed to mitigate/prevent the threat in the misuse cases. This assignment also gave us the opportunity to do deeper research into the existing documentation for ERPNext. 
