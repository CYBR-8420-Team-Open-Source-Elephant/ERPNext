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


## Reflection
Across the individual reflections, a common theme included the value that the use/misuse diagrams provided throughout the assignment process. These allowed for the team to visualize and trace the interactions occurring between the actors and software. These interactions included threat use/misuse cases that the software could potentially interact with in the real world. These visualizations also allowed us to better identify the security requirements that are needed to mitigate/prevent the threat in the misuse cases. This assignment also gave us the opportunity to do deeper research into the existing documentation for ERPNext. 
