---
eleventyComputed:
  title: Creating {{ en.ANYID }} Provider Templates
  description: Learn how to create {{ en.ANYID }} provider templates.
  order: 20
---

So you've created some ***action scripts*** and are ready to develop the {{ en.ANYID }} ***template*** in {{ en.DVLS }}. It's time to bring all that hard work into the {{ en.ANYID }} ***template***.

{{ en.ANYID }} ***providers*** are part of the {{ en.DVPAM }} module and can be found under **Administration** —> **Privileged Access** —> **Providers**.

![1](<image link here>)

You'll see the **Template** button in the upper-right corner.

![2](<image link here>)

Clicking the **+** on the **AnyIdentity Templates** screen will bring you to a box to start building your ***template*** with all the common properties and ***actions*** you should be familiar with now.

![3](<image link here>)

You'll start by providing a name and description and enabling all the ***actions*** you want this ***provider*** to implement.

{% snippet, "badgeInfo" %}
Although you're not required to enable each ***action***, Devolutions recommends you do so to see the full benefit of an {{ en.ANYID }} ***provider***.
{% endsnippet %}

### Properties

To manage privileged ***accounts*** on ***identity providers***, {{ en.ANYID }} must authenticate and connect to the ***provider*** through the ***provider's*** endpoint and read/manage ***accounts*** on that ***provider***.

{{ en.ANYID }} must represent the ***identity provider*** itself and ***accounts*** on that ***identity provider*** internally to manage the ***provider*** and pass information back and forth to the ***action scripts*** accurately; it does so with **Properties**.

There are two types of **Properties** in any {{ en.ANYID }} ***provider***: **Provider** and **Account**.

- **Provider Properties**

    ***Provider*** properties define {{ en.ANYID }}'s attributes to authenticate and connect to an ***identity provider***. ***Provider*** properties could be username, password, hostname, or any other unique property to an ***identity provider***.

    To create a ***Provider*** property, click on **Provider Properties** on the {{ en.ANYID }} ***provider*** Template screen and add a property by clicking **Add property**. Then, define the name, type, and whether the property should be mandatory.

    {% snippet, "badgeInfo" %}
    Properties usually match your ***action script*** parameters. Suppose you have ***action scripts*** with parameter names IdentityProviderEndpoint, IdentityProviderEndpointUserName, and IdentityProviderEndpointPassword. In that case, you can use those same names as properties for simplicity.
    {% endsnippet %}

    ![4](<image link here>)

- **Account Properties**

    ***Identity providers*** hold various ***accounts*** or identities. ***Account*** properties are attributes related to a single ***account*** on an ***identity provider***. Common ***account*** properties are ID, Username, and Secret.

    ***Account*** properties identify ***provider accounts*** uniquely and provide a value to store an ***account's*** password or other secure credential.

    Creating ***Account*** properties is identical to creating ***provider*** properties.

### Script Parameters

All ***actions*** have associated ***action scripts*** with at least two to three parameters. {{ en.ANYID }} needs to know how to map a Property to a script parameter to define a relationship between the {{ en.ANYID }} object (***provider*** or ***account***) and each ***action script***.

Script parameters allow you to tell {{ en.ANYID }} what parameters each of your ***action scripts*** has and what {{ en.ANYID }} property that script parameter should be mapped to.

To create a new **Script Parameter**, click on the parent ***action*** and click on **Add script parameter**. Script parameters should mirror your ***action script*** parameters.

### Adding Action Scripts

Once you've defined all of the properties and script parameters, the final and easiest part of creating an {{ en.ANYID }} ***provider template*** is adding the ***action scripts***.

Assuming you've already created the ***action scripts*** outside of {{ en.DVLS }}, you simply need to open each ***action***, click the **Edit** button and paste the ***action script*** verbatim.

![5](<image link here>)

Once you've pasted in each ***action script***, your ***template*** is complete and it's time to start testing!

### Template Example

To help solidify the concepts covered in this section, below is an example of values for a completed {{ en.ANYID }} ***template*** based on the following ***action scripts***:

```powershell
[CmdletBinding()]
param(
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpoint,
    
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpointUserName,
    
    [Parameter(Mandatory)]
    [securestring]$IdentityProviderEndpointPassword
)
```

```powershell
[CmdletBinding()]
param(
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpoint,
    
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpointUserName,
    
    [Parameter(Mandatory)]
    [securestring]$IdentityProviderEndpointPassword,
    
    [Parameter(Mandatory)]
    [securestring]$NewPassword,
    
    [Parameter(Mandatory)]
    [string]$AccountUserName
)
```

```powershell
[CmdletBinding()]
param(
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpoint,
    
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpointUserName,
    
    [Parameter(Mandatory)]
    [securestring]$IdentityProviderEndpointPassword,
    
    [Parameter(Mandatory)]
    [securestring]$AccountSecret,
    
    [Parameter(Mandatory)]
    [string]$AccountUserName
)
```

## Provider Properties

---

| Property Name | Property Type | Mandatory |
| --- | --- | --- |
| IdentityProviderEndpoint | String | Yes |
| IdentityProviderEndpointUserName | UserName | Yes |
| IdentityProviderEndpointPassword | Password | Yes |

## Account Properties

---

| Property Name | Property Type | Mandatory |
| --- | --- | --- |
| AccountUserName | UniqueIdentifier | Yes |
| AccountSecret | Password | Yes |

## Script Parameter Types

---

| Parameter Name | Action(s) | Property | Source | Mandatory |
| --- | --- | --- | --- | --- |
| IdentityProviderEndpoint | ***Password Rotation***, ***Heartbeat***, ***Account*** Discovery | IdentityProviderEndpoint | ***Provider*** | Yes |
| IdentityProviderEndpointUserName | ***Password Rotation***, ***Heartbeat***, ***Account*** Discovery | IdentityProviderEndpointUserName | ***Provider*** | Yes |
| IdentityProviderEndpointPassword | ***Password Rotation***, ***Heartbeat***, ***Account*** Discovery | IdentityProviderEndpointPassword | ***Provider*** | Yes |
| NewPassword | ***Password Rotation*** | N/A | System | Yes |
| AccountUserName | ***Password Rotation***, ***Heartbeat*** | AccountUserName | ***Account*** | Yes |
| AccountSecret | ***Heartbeat*** | AccountSecret | ***Account*** | Yes |