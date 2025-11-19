# Assurance Cases for Software Security Engineering

[Project Board](https://github.com/orgs/CYBR-8420-Team-Open-Source-Elephant/projects/3/views/1)


---


## Claims

### **Claim 1 - ERPNext’s role-based access control minimizes the risk of permission misconfiguration.**

![Assurance Case - APIs](/Assurance-Case-RBAC.jpg)


**Part 2 Assessment**

The documentation on both Frappe and ERPNext was readily available and clear for my research into how RBAC minimizes the risk of permission misconfiguration. I especially found the documentation regarding the audit trail, permission levels, role based permissions, and custom roles particularly helpful in supporting my top-level claim. An element I would add to fill the gaps in this documentation include task-mapping examples/outlines and audit best practices. These two elements would further support user implementation of the audit trail, permission levels, role based permissions, and custom roles.


----

### **Claim 2 - ERPNext’s user authentication reliably prevents unauthorized access.**


<img width="991" height="1094" alt="Assurance Case- User Authentication drawio (1)" src="https://github.com/user-attachments/assets/69fac9e6-621f-4e92-8fa6-b9eca60c5a66" />



**Part 2 Assessment**  

The documentation for ERPNext has some information to back up the claims provided in the user authentication assurance case. Documentation clearly defines the password requirements as well as session timeouts and reset requirements. It also highlights the availability of the access logs. In terms of gaps and improvement, ERPNext could provide more information on the alerting thresholds when incidents happen and clarity on how session tokens are generated. Since there is no clear evidence of either, there are some potential vulnerabilities that the documentation does not address.

----

### **Claim 3 - ERPNext does not expose sensitive information in public APIs.**

![Assurance Case - APIs](/api-assurance-case.png)

**Part 2 Assessment**  

Much of the evidence that I identified was available in the documentation both for ERPNext and the underlying Frappe framework. Github actions also provided sources of evidence. The GitHub repositories for ERPNext and the Frappe framework use automated actions that provide static code analysis with tools like Semgrep and CodeQL and check for dependencies that are out of date or have known vulnerabilities. The only evidence that required additional efforts to collect was the CVE reports for the application. Finding current CVEs requires searching external databases, but it is understandable that the developers would not publicly disclose vulnerabilities until a fix is available. Overall, the evidence for this claim is readily available.


----

### **Claim 4 - ERPNext ensures the validity of input and external data exchanges.**


![Assurance Diagram of input validity](/Assurance%20Case%20new%20-%20Niazie.png)

**Part 2 Assessment**

All the evidence I found was in the official Frappe and ERPNext documentation. The validation hooks, API authentication methods, and audit trail features are all explicitly described and can be verified directly within a deployed ERPNext instance. There is some pieces of evidence that I would choose to include additional testing for verification such as the Track Changes. The documentation has it clearly described but there isn't a clear, screenshot, proof that warnings appear when disabled. There is also no example log output for the API access log in the documentation so additional verification would be very nice here. The ORM isn't displayed with clear evidence of penetration testing but the code and documentation do more than enough to ensure that this operational evidence is solid.
 
----

## AI Use for Assurance Cases

The following AI prompt was used to enhance the framing of one of our assurance cases:

You are a software engineer. Your job task includes suggesting improvements by phrasing them as assurance claims. Claims include elements of the software that may have security risks or vulnerabilities. A claim needs to be worded with the correct grammar. This grammar includes a predicate. Claims should not be formed in relation to techniques/methods. The claim should have a reachable goal. 

Good claim: “ERPNext role-based access control minimizes the risk of permission misconfiguration.”

Bad claim: “The system uses role-based access control.”

Claim checklist:
Includes relevant argument
Includes critical property of the entity
Includes value for the property 
Includes any related uncertainty of the property

This AI prompt was useful by enhancing the framing of our assurance cases. This prompt was particularly helpful because it showed examples of a good and bad claim. The checklist was also useful in assuring that all the needs of the claim framework were met. Inclusions of the grammar requirements were also useful. This AI prompt was able to provide 18 different possible claims/rebuttals and evidence. This was a great technique in idea generation/deeper research into our project documentation. 

## Team Reflection

This assignment helped us to understand that the trustworthiness of a system should be reasoned rather than assumed. The security features of a system should be used as evidence of a claim about the system rather than boxes that need to be checked. We believe the exercise of developing assurance cases can be useful in the workplace to guide development and to convince stakeholders that software meets their security requirements. We also found that developing a solid argument can be difficult, but receiving feedback from our team members and from AI tools helped us to improve our arguments.