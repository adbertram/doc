---
eleventyComputed:
  title: Windows users provider
---
The Windows Users Provider allows {{ en.DVLS }} to store the Windows account credentials to be used for Windows local accounts discovery or to achieve password rotation. See the [Create Windows users provider](/server/kb/how-to-articles/create-windows-users-provider/) knowledge base article for more information on its configuration.

{% snippet, "badgeInfo" %}
* The [Scheduler service](/server/kb/knowledge-base/scheduler-service-general-information/) must be installed and running to use this feature.
* If you use a different administrator than the default built-in one, you need to enable the "User Account Control: Admin Approval Mode for the Built-in Administrator account" policy. See Microsoft's article for more information: [Description of User Account Control and remote restrictions in Windows Vista](https://learn.microsoft.com/en-us/troubleshoot/windows-server/windows-security/user-account-control-and-remote-restriction).
{% endsnippet %}

![!!ServerOp8089](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp8089.png)

### General
| Option      | Description                  |
|-------------|------------------------------|
| Name        | Display name of the Provider.|
| Description | Description of the Provider. |

### Password settings
| Option                              | Description                                                                                        |
|-------------------------------------|----------------------------------------------------------------------------------------------------|
| Password template used on generation| Password template that will be used to generate the password during the reset password operation.  |

### Host
| Option        | Description                             |
|---------------|-----------------------------------------|
| Computer name | Computer name of the Windows machine.   |

### Credentials
| Option   | Description                                                        |
|----------|--------------------------------------------------------------------|
| Credential type | Custom credentials or Linked credential options.            | 
| Username | Username of the Windows local account with rights to list accounts.|
| Password | Password of the Windows local account.                             |
| Linked credential | Credential directly linked to a PAM account.              |                        

### Actions
| Option                | Description                                                         |
|-----------------------|---------------------------------------------------------------------|
| Add PAM {{ en.VLT }}  | Will create a PAM {{ en.VLT }} with the provider's name if enabled. |
| Add Scan Configuration| Will open the Scan Configuration dialog if enabled.                 |
