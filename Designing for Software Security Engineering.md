# Designing for Software Security Engineering

[Project Board](https://github.com/orgs/CYBR-8420-Team-Open-Source-Elephant/projects/3/views/1)


----


## Data Flow Diagram

----

## Threat Modeling Report


----

## Part 2 Observations

Overall, we found that ERPNext and the underlying Frappe framework have security features that mitigate threats along many data flows. Frappe supports multiple authentication methods ([source](https://docs.frappe.io/framework/user/en/guides/integration/rest_api/simple_authentication)) that protect against threats related to spoofing. ERPNext's role-based permission system ([source](https://docs.frappe.io/erpnext/user/manual/en/role-based-permissions)) can mitigate privilege escalation. ERPNext also has logging features ([source](https://docs.frappe.io/erpnext/user/manual/en/asset-maintenance-log)) that can protect against repudiation. However, we found that many of the mitigations are dependent on proper configuration of the application deployment. This is especially relevant to threats surrounding the database. MariaDB does not encrypt transmissions by default ([source](https://mariadb.com/docs/server/security/securing-mariadb/encryption/data-in-transit-encryption/secure-connections-overview)) and Redis assumes it will be accessed only by trusted clients in a trusted environment in its default configuration ([source](https://redis.io/docs/latest/operate/oss_and_stack/management/security/#security-model)). These may not be concerns if all the ERPNext processes are running on a single, trusted server. However, if ERPNext is set up with the database on a separate server from the Backend Web Server and Background Scheduler/Worker processes, additional configuration would be needed to secure the data flows to and from the database. We found that threats related to excessive resource usage may warrant further investigation, but they could also be in the realm of deployment concerns rather than concerns with the codebase. We also found that threats related to logging may need to be investigated given the importance of audit logs in mitigating other threats.

----

## Team Reflection

