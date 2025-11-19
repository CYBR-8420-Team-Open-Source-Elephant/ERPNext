# Designing for Software Security Engineering

[Project Board](https://github.com/orgs/CYBR-8420-Team-Open-Source-Elephant/projects/3/views/1)


----


## Data Flow Diagram
![Assurance Case - APIs](/Final%20DFD%20ERPNEXT.png)
----

## Threat Modeling Report
[ERPNext Threat Modeling Report](https://htmlpreview.github.io/?https://github.com/CYBR-8420-Team-Open-Source-Elephant/ERPNext/blob/main/ERPNEXT_REPORT.htm)

----

## Part 2 Observations

Overall, we found that ERPNext and the underlying Frappe framework have security features that mitigate threats along many data flows. Frappe supports multiple authentication methods ([source](https://docs.frappe.io/framework/user/en/guides/integration/rest_api/simple_authentication)) that protect against threats related to spoofing. ERPNext's role-based permission system ([source](https://docs.frappe.io/erpnext/user/manual/en/role-based-permissions)) can mitigate privilege escalation. ERPNext also has logging features ([source](https://docs.frappe.io/erpnext/user/manual/en/asset-maintenance-log)) that can protect against repudiation. However, we found that many of the mitigations are dependent on proper configuration of the application deployment. This is especially relevant to threats surrounding the database. MariaDB does not encrypt transmissions by default ([source](https://mariadb.com/docs/server/security/securing-mariadb/encryption/data-in-transit-encryption/secure-connections-overview)) and Redis assumes it will be accessed only by trusted clients in a trusted environment in its default configuration ([source](https://redis.io/docs/latest/operate/oss_and_stack/management/security/#security-model)). These may not be concerns if all the ERPNext processes are running on a single, trusted server. However, if ERPNext is set up with the database on a separate server from the Backend Web Server and Background Scheduler/Worker processes, additional configuration would be needed to secure the data flows to and from the database. We found that threats related to excessive resource usage may warrant further investigation, but they could also be in the realm of deployment concerns rather than concerns with the codebase. We also found that threats related to logging may need to be investigated given the importance of audit logs in mitigating other threats.

----

## Team Reflection

As a team, we learned how valuable analysis of system security can be with the utilization of the Microsoft Threat Modeling Tool. Any movement of data can produce threats. This required us to analyze the data flow to understand where the risks were emerging. It was also helpful to simplify ERPNext through the use of level-0 and level-1 DFD. The core processes and components could be viewed from an architectural stand point, allowing for the data flows to be more clear. We were then able to assess how ERPNext actually behaves, looking a the basic data flow interactions that introduce threats. The assignment also showed the importance of external configurations for hardened security within ERPNext. It was very useful to create multiple draft diagrams and rely on team collaboration to reach our final diagram/threat report. This assignment also allowed us to further research the existing documentation within ERPNext/Frappe. Overall, this assignment allowed for an architectural approach to threat modeling that was very useful going forward with further analysis of ERPNext as a whole. 
