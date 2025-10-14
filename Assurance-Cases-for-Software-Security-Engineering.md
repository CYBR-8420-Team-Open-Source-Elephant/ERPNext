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


##Diagram here

**Part 2 Assessment**

 
----

## AI Use for Assurance Cases




## Team Reflection
