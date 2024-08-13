---
eleventyComputed:
  title: {{ en.ANYID }} Provider Templates
  description: An {{ en.ANYID }} provider template is a "recipe" for building {{ en.ANYID }} providers. 
---

{{ en.ANYID }} ***providers*** are built and managed with [templates](https://github.com/Devolutions/PAM-Providers/tree/master). ***Templates*** allow you to use Devolutions' and the community’s efforts to build providers, so you don’t have to.

A ***template*** is an object within {{ en.DVPAM }} that represents a framework for building an {{ en.ANYID }} ***provider***.

Templates tell {{ en.DVLS }} how to “map” the ***action script*** parameters and output to {{ en.DVPAM }} internal properties to input and pass information back and forth. ***Templates*** allow users to simply fill an ***identity provider***'s properties to create a ***provider***.

***{{ en.ANYID }} provider templates*** are broken down into four sections:

- **General**

    Information like the name, description, and which **actions** to enable.

    ![1](<image link here>)

- **Provider Properties**

    This section contains credentials and other information that will be passed to the ***identity provider***. You will find fields like username, password, hostname, port, etc. The information in this section should be used to connect to the ***identity provider***.

    Here, you will define each **Provider Property** along with its **Type** and whether it should be **Mandatory**.

    The properties defined in this section map to ***provider*** fields within {{ en.DVLS }} to properly pass values at runtime.

    ![2](<image link here>)

    {% snippet, "badgeInfo" %}
    {{ en.DVLS }} provides eight different **Types** with three *required* **Types:** **Username**, **Password,** and **Unique Identifier**.
    ![3](<image link here>)
    {% endsnippet %}

- **Account Properties**

    Attributes relating to a specific account on an ***identity provider***, such as a unique identifier, username, or password.

    The properties defined in this section map to account fields within {{ en.DVPAM }} to properly pass values at runtime.

    ![4](<image link here>)

- **Actions**

    **Parameters** for each ***action*** and a place to paste the ***action***’s PowerShell script. This is the area where you map the parameters in each ***action***’s PowerShell script to the ***Provider*** or **Account Properties** by selecting the **Source** (either ***Provider*** or ***Account***) and the ***Provider*** or **Account Property**.

    All **Parameters** defined in this area will be passed to the defined PowerShell script, including any parameters for connecting to the ***identity provider*** and parameters and any specific account-related parameters like username, password, etc.

    ![5](<image link here>)

    In the example above, the associated PowerShell script would have parameters defined like the below. You can see that the PowerShell parameter types are mapped to the **Provider Property Types** defined under **Provider Properties**.

    ```powershell
    [CmdletBinding()]
    param(
        [Parameter()]
        [string]$ProviderUserName,
        
        [Parameter()]
        [securestring]$ProvierPassword,
        
        [Parameter()]
        [string]$Server,
        
        [Parameter()]
        [string]$Instance,
        
        [Parameter()]
        [int]$Port,
        
        [Parameter()]
        [string]$UserName,
        
        [Parameter()]
        [securestring]$Secret
    )
    ```
