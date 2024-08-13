---
eleventyComputed:
  title: Adding a PAM provider
  description: Learn how to add a PAM provider.
  order: 10
---

In ***Administration – Privileged Access – Providers***, add a provider. The available types are:

* ***Managed*** providers: ***Domain User*** (AD), ***Local User*** (SSH), ***SQL Server***, ***Windows User***, ***Azure AD User***
* ***Password reset only*** (unmanaged) providers: ***MySQL User***, ***Cisco User***, ***Oracle User***
* ***AnyIdentity*** providers: ***Windows Accounts***, ***Windows Local Accounts***

![Managed PAM providers](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2107.png) ![Password reset only PAM providers](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2108.png) ![AnyIdentity PAM providers](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2109.png) When adding the provider, make sure to enable the ***Add PAM {{ en.VLT }}*** and ***Add Scan Configuration*** options under ***Actions***. ![PAM provider configuration](https://cdnweb.devolutions.net/docs/docs_en_server_ServerOp2110.png)

{% snippet, "badgeHelp" %}
For more information, please refer to [Providers](/pam/server/providers/).
{% endsnippet %}

When you click ***Save***, the ***Scan Configuration*** appears.