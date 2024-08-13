---
eleventyComputed:
  title: Import accounts from a scan configuration
  description: 
  order: 30
---

Once you have a list of ***accounts*** discovered, it’s now time to import privileged ***accounts*** into a {{ en.DVPAM }} {{ en.VLT }}. If you selected to create a {{ en.VLT }} when creating the ***provider***, you will have one created with the same name as the ***provider*** otherwise you’ll have to [create one yourself](https://docs.devolutions.net/pam/hub/pam-vaults/#pam-vault-setup).

To import ***accounts*** into a {{ en.VLT }}, you’ll select each discovered user and click on **Import Selected Accounts**.

![1](<image link here>)

You’ll then select the **Provider** and the **Path** to the {{ en.VLT }} to add the ***accounts*** to.

![2](<image link here>)

If you'd like to reset passwords immediately on all imported ***accounts***, check the **Reset Password on import** option. This option will automatically run a ***heartbeat*** and ***password rotation action*** on every ***account*** imported.

Clicking **OK** will then import the ***accounts***(s) into the {{ en.VLT }}.

Once imported, you should then see the ***account*** show up under the ***provider***’s {{ en.VLT }}.

![3](<image link here>)

## Verifying Heartbeat and Password Rotation Actions On Import

At this point, the ***provider*** should have run the ***heartbeat*** and ***password rotation actions*** checking and resetting the password of accounts if the **Reset Password on import** was selected. Let’s verify.

To verify, click on the ***account*** and then on the **Logs** category.

![4](<image link here>)

Within the logs, you should see three messages:

- **Entry added** - This message indicates a new ***account*** has been added to the {{ en.VLT }}.
- **PAM Password reset - Success** - This message indicates the ***provider*** ran the ***password rotation action*** and it has successfully changed the password.
- **Check synchronization - Success** - This message indicates that the ***heartbeat action*** compared the current password that {{ en.DVPAM }} has with the password assigned to the ***account*** and they matched.

If you see each of these messages, you can confirm that the ***provider*** has successfully run all ***actions***!

Although importing a new ***account*** into a {{ en.VLT }} will automatically run a ***heartbeat*** and ***password rotation action***, you can also test both ***actions*** at any time.

While viewing the ***account*** in the {{ en.VLT }}, you can test the ***heartbeat action*** by right-clicking on the ***account*** and clicking on **Check Synchronization Status** (1) or by clicking on the atom symbol (2) as shown below.

![5](<image link here>)

If successful, you will see the **Check synchronization - Success** message in the ***account*** logs.
