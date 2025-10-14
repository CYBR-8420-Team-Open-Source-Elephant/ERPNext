# Assurance Cases for Software Security Engineering

[Project Board](https://github.com/orgs/CYBR-8420-Team-Open-Source-Elephant/projects/3/views/1)


---


## Claims

### **Claim 1 - ERPNext’s role-based access control minimizes the risk of permission misconfiguration.**

##Diagram here


**Part 2 Assessment**


----

### **Claim 2 - ERPNext’s user authentication reliably prevents unauthorized access.**

##Diagram here


**Part 2 Assessment**  


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




## Team Reflection
