---
eleventyComputed:
  title: AnyIdentity Providers
  description: 
---

Sometimes ***action scripts*** fail for numerous reasons while in {{ en.ANYID }} and it's important to know how to track down the issue. Multiple issues can arise for an {{ en.ANYID }} ***provider*** because of the various steps involved. Complicating matters, {{ en.ANYID }} heavily relies on your ***action scripts*** for functionality and depending on your ***identity provider***, ***action scripts*** can become complex.

There are a lot of ways problems could arise if you don't thoroughly test the ***provider*** ahead of time. Let's cover where to look for issues and how to troubleshoot any problems that may come up.

1. **Identity the problem.**

    Sometimes the problem may not be so obvious. Your ***action script*** may be working great on their own but you might find out that {{ en.ANYID }} isn't actually applying password changes as you expect. For example, if your ***action scripts*** are built incorrectly and return false information, {{ en.ANYID }} will use this information to make decisions and think all is well when it is not.

    But sometimes, the issue is more obvious, you could see an **Out of sync** message for the user in the {{ en.DVPAM }} ***vault*** or see a problem in the logs.

    ![1](<image link here>)

2. **Identity the ***action script*** involved.**

    Since {{ en.ANYID }} is essentially a script orchestrator, 90% of it's functionality depends on your ***action scripts***. If you see an error come up in the {{ en.DVLS }} console, you should first try to identity which ***action script*** was involved. To do so, you need to understand how {{ en.ANYID }} "maps" functionality to the ***action scripts*** with it's terminology.

    - **Scan configuration** - ***Scan configurations*** use the ***account discovery*** ***action script***.
    - **Synchronization** - {{ en.ANYID }} uses the term "synchronization" to indicate running the ***heartbeat*** ***action script***.
    - **Password Reset** - When you initiate a password reset in {{ en.ANYID }}, that uses both the ***password rotation*** and ***heartbeat*** ***action scripts***.

3. **Test ***action scripts*** outside of {{ en.ANYID }}.**

    Once you've discovered which ***action scripts*** are involved, you first need to test them outside of {{ en.ANYID }} to ensure the problem doesn't lie in the ***action script*** itself. Pass the same parameters to the script as you've defined via **Script Parameters** when creating the ***template***. Ensure the PowerShell script returns what {{ en.ANYID }} expects:

    - **Account discovery** - Should output at least one `pscustomobject` object with an `id`, `username` and `secret` property.
    - **Heartbeat** - Should have `username` and `secret` parameters and return either a single boolean `$true` or `$false`.
    - **Password rotation** - Should have parameters for ***identity provider*** endpoint, endpoint username, endpoint password and a specifically named parameter called `NewPassword`.
