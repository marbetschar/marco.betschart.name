---
description: My contributions to elementary Mail during the month.
---

# A month full of elementary Mail

_July 2021_

![elementary Mail](../.gitbook/assets/io.elementary.mail.png)

{% hint style="info" %}
If you like my contributions, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

What a month! Passed my exams, went on holiday and still got plenty of time to give elementary Mail some love. In case you are not aware yet: elementary Mail was rewritten from scratch to integrate with the local Evolution Data Server backend. This is the very same backend powering elementary Calendar and elementary Tasks. So, what exactly can you expect from my work this month?

### Support for Well Known Folders

Quite a few elementary Mail features rely well known folders such as `Inbox`, `Drafts`, `Archive` and `Sent`. That said, it is crucial to correctly detect those folders upon setup - otherwise parts of the user interface will not work as expected. As it turned out, detecting those folders is quite a challenge since different mail providers adhere to different naming schemes. However, in the latest version of Mail [most of the folders should be recognized correctly most of the time](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/192).

### Store copy of sent mail in Sent folder

Even though sending emails already worked in elementary Mail, it did not always store a copy of the sent mail in the `Sent` folder. I fixed this in the latest version of elementary Mail and you can expect all sent mails to be stored correctly in the Sent folder - regardles off your mail provider. Please note: This was a non-issue for Office 365 and Gmail users.

### Handle reply subject

elementary Mail now [correctly displays the subject field](https://github.com/elementary/mail/pull/602) whenever you forward or reply to an email. In addition Mail does now [handle `Re:` subject prefixes correctly](https://github.com/elementary/mail/pull/603) whenever you hit the reply button.

### Save draft

Up until now, the new elementary Mail was not capable of saving a draft. Inevitably mails got lost because they were not sent. Now elementary Mail [automatically saves](https://github.com/elementary/mail/pull/599) the draft whenever you leave the compositor.

### Edit draft

Saving drafts is fine to avoid data loss. However, they are even more useful if they can be edited again. This feature is exactly what [my Pull Request #626](https://github.com/elementary/mail/pull/626) is going to add. Its not quite done yet, but its nearly there!

### Online Accounts: Verify credentials

And one more thing: The mail account setup in `System Settings > Online Accounts` does now [verify your IMAP/SMTP credentials before they got saved](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/189). Once the setup is sucessful, you can be sure the mail account actually works in elementary Mail. This fixes a bunch of issues where users did not see any mails - even though the Online Accounts setup (wrongly) indicated it was sucessful.