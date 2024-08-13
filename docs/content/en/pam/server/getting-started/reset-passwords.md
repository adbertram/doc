---
eleventyComputed:
  title: Reset passwords
  description: Learn how to reset passwords for accounts in a {{ en.VLT }}.
  order: 40
---

To reset an ***account*** password manually, right-click on the ***account*** in the {{ en.VLT }}, hover your mouse over **More** and choose **Reset password** (1) or click on the three dots on the upper right part of the screen and click on **Reset Password** (2).

![1](<image link here>)

If the ***password rotation action*** worked, you’ll see the **PAM Password reset - Success** message in the logs.

{% callout, "badgeInfo" %}
When you reset a password for an ***account***, this task invokes both the ***password rotation action*** and then the ***heartbeat action*** to verify the password rotation actually succeeeded.
{% endcallout %}
