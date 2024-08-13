---
eleventyComputed:
  title: Logs
  description: Logs are a way to monitor the activity of a provider.
---

When ***providers*** execute ***actions***, those ***actions*** are recorded to a set of logs you can inspect within {{ en.DVLS }}. You can find all logs within the **Reports** section in {{ en.DVLS }}.

- **Privileged Access Logs**

    Once an ***account*** has been imported into a {{ en.DVPAM}} ***vault***, you will start to see activity in the Privileged Acesss Logs.

    ![1](<image link here>)

    This log is where you'll see activity both for individual ***accounts*** and what's going on with the ***provider*** itself.

    ![2](<image link here>)

    Here is where you will get insight into both the ***heartbeat*** and ***password rotation*** activity ***accounts***.

- **Data source logs**

    When a problem arises in any {{ en.ANYID }} ***action script***, for example, you may see activity in the data source logs. This is where more general information is logged. It is also where you'll see specific error messages ***action scripts*** return.

    ![3](<image link here>)

    ![4](<image link here>)
