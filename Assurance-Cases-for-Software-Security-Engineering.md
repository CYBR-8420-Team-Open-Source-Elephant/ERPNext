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

##Diagram here

**Part 2 Assessment**  


----

### **Claim 4 - ERPNext ensures the validity of input and external data exchanges.**


![Assurance Diagram of input validity](/Assurance%20Case%20new%20-%20Niazie.png)

**Part 2 Assessment**

All the evidence I found was in the official Frappe and ERPNext documentation. The validation hooks, API authentication methods, and audit trail features are all explicitly described and can be verified directly within a deployed ERPNext instance. There is some pieces of evidence that I would choose to include additional testing for verification such as the Track Changes. The documentation has it clearly described but there isn't a clear, screenshot, proof that warnings appear when disabled. There is also no example log output for the API access log in the documentation so additional verification would be very nice here. The ORM isn't displayed with clear evidence of penetration testing but the code and documentation do more than enough to ensure that this operational evidence is solid.
 
----

## AI Use for Assurance Cases




## Team Reflection
