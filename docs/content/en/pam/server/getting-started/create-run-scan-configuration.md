---
eleventyComputed:
  title: Create and run a scan configuration
  description: 
  order: 20
---

A ***scan configuration*** is a set of instructions that dictate what ***provider*** to use and a way to set an optional recurrence schedule to periodically run the ***account discovery action*** on that ***provider***.

Under **Administration** —> **Privileged Access** —> **Scan Configurations** is where you will find all existing ***scan configurations*** and the ability to create a new one. To create a new ***scan configuration***, click on the target with the plus symbol in the upper-right corner of the screen.

![1](<image link here>)

***Scan configurations*** apply to both managed and {{ en.ANYID}} providers. Here you can choose either.

![2](<image link here>)

Pick the provider, set the name and click **OK**.

![3](<image link here>)

{% snippet, "badgeInfo" %}
Although you can create a ***scan configuration*** with any name you’d like, it’s best to name it based on the ***provider*** it’s a part of.
{% endsnippet %}

When you create the ***scan configuration***, it will queue a job. You can see that it’s queued by the hourglass icon next to the job. The job is scheduled by the *{{ en.DVLS }}* Windows service on the {{ en.DVLS }} host. Depending on the backlog, this process make take a few minutes.

![4](<image link here>)

Once the job is complete, you should see the **Status** is now a green check mark with a number of **Results**.

![5](<image link here>)

Each result is an ***account*** that the ***account discovery action*** found. If you see results at this point and they match what the ***account discovery action*** returned, ***account discovery action*** is working!

Clicking on the **Results**, you’ll see all of the ***accounts*** the ***account discovery action*** found.

![6](<image link here>)

{% snippet, "badgeInfo" %}
For more information, please refer to [***Scan configurations***](/pam/scan-configurations/).
{% endsnippet %}
