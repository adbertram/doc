---
_schema: default
eleventyComputed:
  title: Getting started
  description: >-
    To get started with the Privileged Access Management (PAM) features of {{
    en.DVLS }}, first log in as an administrator in your {{ en.DVLS }}.
---
To get started with the ***Privileged Access Management*** (PAM)features in {{ en.DVLS }}, first log in as an administrator in your {{ en.DVLS }}. Then, follow the steps below.

## Configure PAM settings

1. In {{ en.DVLS }}, head to ***Administration – Licenses***.
2. Add your PAM license using the ***Add*** (+) button. When done, the license appears in the license list and the Privileged Access menu appears in the side panel of your {{ en.DVLS }}. ![PAM license](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2104.png)
3. In ***Administration – Privileged Access – Default settings***, configure the settings for the [{{ en.VLT }} visibility](/server/web-interface/vault-access/), [checkout system](/pam/server/checkout-process/request-checkout/), [credentials brokering](/pam/server/view-sensitive-data-account-brokering/), [sensitive information access](/pam/server/view-sensitive-data-account-brokering/), default checkout times, and synchronizations. ![Administration – Privileged Access – Default settings](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2105.png)
4. Next, head to ***Administration – System Permissions – Modules***.
5. Configure access to the PAM system for users/admins and manage privileged accounts rights on who can edit the privileged entries. Then, click ***Save***. ![Administration – System permissions – Modules – Privileged access](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2106.png)

## Add a scan configuration

1. Confirm that it is the correct provider, domain name, and domain container (where the accounts are located).
2. Make sure the ***Start Scan on Save*** option is enabled under ***Actions***.
3. Click ***OK***. ![PAM Scan configuration](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2111.png)



## Import accounts from a scan

