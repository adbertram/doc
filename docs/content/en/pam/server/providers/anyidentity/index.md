---
eleventyComputed:
  title: {{ en.ANYID }} Providers
  description: {{ en.ANYID }} providers are an extension of {{ en.DVPAM }} managed providers and are meant to close the gap between the {{ en.DVPAM }} supported identity providers and the plethora of other identity providers that Devolutions customers may be using.
  order: 10
---

{{ en.DVPAM}} offers many managed providers but will not and cannot possibly support every ***identity provider***: this is where {{ en.ANYID }} ***providers*** come in.

{{ en.ANYID }} ***providers*** are an extension of ***managed providers*** and are meant to close the gap between the ***identity providers*** that the {{ en.DVPAM }} module natively supports through ***managed providers*** and the plethora of other ***identity providers*** that Devolutions customers may be using.

An {{ en.ANYID }} ***provider*** could support any number of ***identity providers*** not natively supported by {{ en.DVPAM }}, such as:

- **Cloud-based identity providers** like Okta or Google Workspace manage access to cloud applications and services.
- **Custom applications:** Any in-house system your organization has developed that maintains its own user database and authentication mechanisms.
- **Legacy systems:** Older applications or databases that might not integrate easily with modern identity management solutions.

{{ en.ANYID }} ***providers*** have various ***actions*** written in PowerShell called ***action scripts*** that are executed either on-demand or on a scheduled basis via ***scan configurations*** to discover ***identity provider*** credentials, detect credential changes, and rotate passwords for credentials.

- ***Account discovery*** - Enumerates credentials on an ***identity provider***
- ***Heartbeat*** - Detects if a credential has changed since the last heartbeat
- ***Password rotation*** - Changes account passwords to a new, secure password

If you can write PowerShell, you can build {{ en.ANYID }} ***providers*** or use any of the [pre-built templates](https://github.com/Devolutions/PAM-Providers).

![{{ en.ANYID }} provider](https://cdnweb.devolutions.net/docs/DVLS4026_2024_2.png)
