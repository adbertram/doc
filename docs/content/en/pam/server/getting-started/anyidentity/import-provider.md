---
eleventyComputed:
  title: Import an {{ en.ANYID }} provider
  description: Learn how to import an {{ en.ANYID }} provider.
  order: 10
---

To create the provider, you’ll first navigate to the **Privileged Access** section in {{ en.DVLS }} and clicking on **Providers**.

![1](<image link here>)

Click on the **+** sign in the upper-right corner to **Add** the ***provider***.

![2](<image link here>)

Next, click on **AnyIdentity** and then on your ***template***. Here you'll see an existing ***provider template*** called **Microsoft SQL Server Login**.

![3](<image link here>)

Your next step is defining a name and providing values for all of the ***Provider properties***. You can see from the screenshot below that the **Server** provider property is defined as Mandatory in the ***template***; you can tell by the red asterisk and red box around the field.

![4](<image link here>)

{% snippet, "badgeInfo" %}
{{ en.ANYID }} ***providers*** assume you’ll be connecting to a single ***identity provider endpoint***. Generally, you should build one {{ en.ANYID }} ***provider*** per ***identity provider***.
{% endsnippet %}>

After you’ve provided values for all of the ***provider properties***, you then have the option to add a [PAM vault](https://docs.devolutions.net/pam/hub/pam-vaults/#pam-vault-setup) for the ***provider*** or add a ***scan configuration***. By default, **Add PAM Vault** is selected. For now, we’re not going to add a ***scan configuration***. You can learn more about ***scan configurations*** [here](/pam/scan-configurations/).

![5](<image link here>)

On this page, you may also specify a credential to run all ***actions*** under or a specific Windows host to run on.

![6](<image link here>)

{% snippet, "badgeInfo" %}
By default, an {{ en.ANYID }} ***provider*** runs all actions on {{ en.DVLS }} under the NETWORK SERVICE user account. If you specify a username and password under **Run As**, {{ en.ANYID }} will attempt to first authenticate to the {{ en.DVLS }} server using that user account and run all action scripts under that account. If you specify a **Host Name**, {{ en.ANYID }} assumes a remote Windows host and will attempt to run all ***action scripts*** locally on that host via [PowerShell Remoting](https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/08-powershell-remoting?view=powershell-7.4).
{% endsnippet %}

And finally, under **Settings**, you can provide a custom [***password template***](https://docs.devolutions.net/rdm/commands/file/templates/password-templates/), if necessary. You can find all available custom ***password templates*** under **Administration** —> **Password Templates**. When the ***password rotation action*** runs, it will use the ***password template*** defined here to generate a new password.

![7](<image link here>)