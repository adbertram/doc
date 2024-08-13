---
eleventyComputed:
  title: Creating {{ en.ANYID }} Action Scripts
  description: Learn how to create {{ en.ANYID }} PowerShell action scripts.
  order: 10
---

If you need a custom {{ en.ANYID }} ***provider***, you'll first have to build the ***action scripts*** that the ***provider*** ***actions*** will execute. Your ***action scripts*** will be what you paste into the Script section of each ***action*** when you buid the ***template***.

***Action scripts*** are just PowerShell scripts that {{ en.DVPAM }} executes, so the same scripting best practices apply as any other PowerShell script, but ***action scripts*** have a few nuances you need to account for when writing them.

{% snippet, "badgeInfo" %}
You must know how to write PowerShell scripts to create {{ en.ANYID }} providers. Devolutions recommends you are at least an intermediate scripter to begin creating action scripts.
{% endsnippet %}

### Identity Provider Endpoint Script Parameters

Every ***action script*** you create must have at least a few parameters for the {{ en.ANYID }} ***provider*** to pass values to. Although each ***action script***'s parameters will differ (examples below), each will have a common set of parameters required to connect to the ***identity provider endpoint***.

Each ***action script*** connects to an ***identity provider***. To do that, the scripts must have the necessary credentials passed to them from the {{ en.ANYID }} ***provider***.

Below is an example of how you can create these ***identity provider*** endpoint parameters.

```powershell
[Parameter(Mandatory)]
[string]$IdentityProviderEndpoint,

[Parameter(Mandatory)]
[string]$IdentityProviderEndpointUserName,

[Parameter(Mandatory)]
[securestring]$IdentityProviderEndpointPassword
```

Although you're welcome to call ***action script*** parameters whatever you like (as long as they match what you provide when building the {{ en.ANYID }} ***template***), we recommend a set of standard parameters to keep a descriptive naming convention.

Notice that each parameter is mandatory. This ensures that the {{ en.ANYID }} ***provider*** is forced to use these parameters. Also, notice the type (`securestring`) for the `IdentityEndpointPassword` parameter. {{ en.ANYID }} requires you to use a `securestring` type to prevent passing and processing any plaintext passwords in the ***action scripts***.

When you create the {{ en.ANYID }} ***template***, these ***identity provider*** endpoint parameters will then map to the **Parameters** you define while building the {{ en.ANYID }} ***template***.

![1 - ***Password rotation*** parameters with the required **NewPassword** parameter (only for password rotation)](<image link here>)

### Handing Optional, Default Parameters

When you need to provide the ability to pass a value to a script parameter but not require it, that parameter is considered optional. It's only used when a value is passed to it.

When creating an {{ en.ANYID }} ***template***, you can define ***provider*** and ***account*** properties and choose to make them either mandatory or optional.

![2 - Optional provider properties **Port** and **Instance**](<image link here>)

An ***action script***'s parameters for the ***provider*** above may look something like below, with each script parameter matching the {{ en.ANYID }} ***template***'s properties and assigning a default value to the optional parameters.

```powershell
[CmdletBinding()]
param(
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpoint,
    
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpointUserName,
    
    [Parameter(Mandatory)]
    [securestring]$IdentityProviderEndpointPassword,
    
    [Parameter()]
    [string]$Instance = '.',
    
    [Parameter()]
    [int]$Port = 1433
)

Write-Host "Using the instance of [$Instance] and the port of [$Port] here in the code somewhere."
```

If you were to execute this PowerShell script outside of {{ en.ANYID }} without using the optional parameters, the script would execute as expected using the default parameter values.

```powershell
.\actionscript.ps1 -IdentityProviderEndpoint 'hostname' -IdentityProviderEndpointUserName 'admin' -IdentityProviderEndpointPassword (ConvertTo-SecureString -String 'P@$$word' -AsPlainText -Force)
```

![3](<image link here>)

But, when you create the {{ en.ANYID }} ***template*** providing only the mandatory parameters and relying on the default parameters within the script, you'll see that {{ en.ANYID }} overwrites the default values.

![4](<image link here>)

When {{ en.ANYID }} executes an ***action script***, it will always pass values on to *all* parameters. Even when you don't define a value, {{ en.ANYID }} will pass `null` values or, if the parameter is an integer, a `0` value.

To prevent this, you must not provide the default values in the script parameters but rather as a condition inside the script's code.

```powershell
[CmdletBinding()]
param(
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpoint,
    
    [Parameter(Mandatory)]
    [string]$IdentityProviderEndpointUserName,
    
    [Parameter(Mandatory)]
    [securestring]$IdentityProviderEndpointPassword,
    
    [Parameter()]
    [string]$Instance,
    
    [Parameter()]
    [int]$Port
)

if (!$Instance) { $Instance = '.' }
if (!$Port) { $Port = 1433 }

Write-Output "Using the instance of [$Instance] and the port of [$Port] here in the code somewhere."
```

Although not recommended for PowerShell best practices, it is a requirement for {{ en.ANYID }} to use default parameter values.

![5](<image link here>)

### Handling Output

Ultimately, ***action scripts*** are executed within {{ en.ANYID }}. Any output these scripts create is interpreted, saved, and/or displayed in the {{ en.DVLS }} web interface.

To ensure that the ***action scripts*** display the output you expect, your ***action scripts*** should only return output four ways:

- The `throw` keyword to throw a terminating error using the error stream
- The `Write-Error` cmdlet to return a non-terminating error using the error stream
- The `Write-Output` cmdlet to return information to the output stream
- Outputting information directly to the output stream

Below are some examples of an ***action script*** and what results you will receive from {{ en.ANYID }}'s **Test Script** functionality's **Results** area.

```powershell
Write-Verbose -Message 'This is a verbose message'
Write-Information -MessageData 'information action'
Write-Output 'output stream here'
Write-Host 'write-host output here'
Write-Error 'error'
```

![6](<image link here>)

```powershell
Write-Verbose -Message 'This is a verbose message'
Write-Information -MessageData 'information action'
Write-Output 'output stream here'
'output stream here directly'
Write-Host 'write-host output here'
```

![7](<image link here>)

{% snippet, "badgeInfo" %}
If you want your ***action script*** to return information to {{ en.ANYID }}, never use `Write-Verbose`, `Write-Information` or `Write-Host`.
{% endsnippet %}

### Account Discovery

The first ***action*** an {{ en.ANYID }} ***provider*** executes is the ***Account Discovery*** ***action***. This ***action*** enumerates ***accounts*** on an ***identity provider*** and populates the {{ en.DVLS }} database for future management.

- **Required Input Parameters**

    The ***action script*** for the ***Account Discovery*** ***action*** is the simplest as it only needs common endpoint script parameters. It does not require any other parameters other than any necessary parameters dependent on a specific ***identity provider***.

- **Required Output**

    The ***account*** discovery script *does* need to return a specific output. Every ***account*** discovery ***action script*** must return one or more `PSCustomObject` type objects, each representing a single ***account*** with three properties:

  - `id` - The `id` property must be a unique identifier for each ***account***. This identifier is usually a username, but it can be anything as long as it's unique to each ***account***.
  - `username` - The `username` property must be a "label" for each ***account***. This value is usually a username, but it can be any label you'd like to represent each ***account***.
  - `secret` - The `secret` property is the password identifier. It can be an encrypted string or even the password in plaintext. It will be used to compare with other secrets via the ***heartbeat*** ***action***.

    If your ***identity provider*** code does not natively return this object with these specific object properties, you must "convert" it by creating a `PSCustomObject` type yourself. Below is one such method.

    ```powershell
    ## some code that returns an object for each account
    $accounts = Get-AccountFromIdentityProvider 
    
    ## create custom fields for Select-Object to reeturn the id and username properties instead of name, and name
    $selectProps = @(
        @{'n'='id';e={$_.name}} ## "convert" the name property from the account to id
        @{'n'='username';e={$_.name}} ## "convert" the name property from the account to username
        @{'n'='secret';e={$_.password_hash}} ## "convert" the password_hash property from the account to secret
    )
    
    ## Pass each account to Select-Object to return the property property names
    $accounts | Select-Object -Property $selectProps
    ```

    When you create an {{ en.ANYID }} ***template*** and test it (instructions below) with a [***scan configuration***](https://docs.devolutions.net/pam/server/scan-configurations/), the **Username,** and **Unique Identifier** fields will be populated with the property values for the `username` and `id` properties from the ***action script***.

![8](<image link here>)

### Heartbeat

Once the Account Discovery ***action*** retrieves all ***accounts*** from the ***identity provider***, the ***Heartbeat*** ***action*** comes into play. The ***Heartbeat*** ***action*** reads an ***account***'s current password value and compares it to PAM's current value. If the two values are different, a change is detected.

- **Required Input Parameters**

    In addition to the common endpoint parameters, a ***heartbeat*** ***action script*** must have at least two parameters:

  - **UserName** - The value of the `username` property the ***account*** discovery ***action script*** returns. This is a `string` parameter.
  - **Secret** - The value of the `secret` property the ***account*** discovery ***action script*** returns. This is a `securestring` parameter.
- **Required Output**

    A ***heartbeat*** ***action script*** only returns a single boolean object (`$true` or `$false`) to indicate whether the current value of an ***account***'s password matches what the PAM modules know.

Below is an example of a ***heartbeat*** ***action script***.

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
    [string]$UserName,
    
    [Parameter(Mandatory)]
    [securestring]$Secret
)

## Code to query for a single user account here. Let's say it's $account

## Convert the password to a secure string
$secPw = $account.password | ConvertTo-SecureString -AsPlainText -Force

## Compare the results
$secPw -eq $Secret
```

### Password Rotation

When {{ en.ANYID }} runs the ***heartbeat*** ***action***, and the ***heartbeat*** ***action script*** returns a `$false` value indicating that the new password {{ en.ANYID }} has is different than the password on the ***identity provider***, the ***password rotation*** ***action*** kicks in.

The ***password rotation*** ***action*** is responsible for syncing passwords generated from the PAM module to the ***identity provider***.

- **Required Input Parameters**

    In addition to the common endpoint parameters, a ***password rotation*** ***action script*** requires one parameter: `NewPassword`. This is a `securestring` parameter that allows {{ en.ANYID }} to pass the value for the new password to the ***action script***.

- **Required Output**

    The ***password rotation*** script should only return a boolean `$true` value if the password change is successful.

Below is a simple example of a ***password rotation*** ***action script***.

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
    [securestring]$NewPassword
)

## $result = Dowhatevertochangethepasword
if ($Result) {
    $True
} else {
    Write-Error "Failed to Update Secret"
}
```
