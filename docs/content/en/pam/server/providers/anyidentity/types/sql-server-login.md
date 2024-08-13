---
eleventyComputed:
  title: SQL Server Login
  description: The SQL Server Login {{ en.ANYID }} ***provider*** allows you to manage SQL Server logins.
---

This SQL Server Login {{ en.ANYID }} ***provider*** is designed to integrate with the {{ en.DVPAM}} module to manage SQL Server login credentials. It enables automated account discovery and password rotation for SQL Server logins.

This ***provider*** allows for:

- Account Discovery: Automated enumeration of SQL Server login accounts.
- Heartbeat: Validation that the passwords in {{ en.DVLS }} match those set on the SQL Server instance.
- Password Rotation: Automated update of SQL Server login passwords as per policy or on-demand.

You can find the pre-built template for this {{ en.ANYID }} ***provider*** [here](https://github.com/Devolutions/PAM-Providers/tree/master/Providers/sql_server_login).