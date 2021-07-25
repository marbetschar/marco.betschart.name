---
description: A month full of elementary Mail
---

# A month full of elementary Mail

_July 2021_

![elementary Mail](../.gitbook/assets/io.elementary.mail.png)

{% hint style="info" %}
If you like my contributions, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

What a month! Passed my exams, went on holiday and still got plenty of time left to provide some love to the all new elementary Mail. In case you are not aware yet: elementary Mail was rewritten from scratch to integrate with the local Evolution Data Server backend. This is the very same backend elementary Calendar as well as elementary Tasks are using for synchronization. So, what exactly can you expect from my work this month?

### Support for well known folders

Quite a few elementary Mail features rely on a handful well known folders such as `Inbox`, `Drafts`, `Archive` and `Sent`. That said, it is crucial to correctly detect those folders upon setup - otherwise parts of the user interface will not work as expected. As it turned out, detecting those folders is quite a challenge since different mail provider adhere to different naming schemes. However, in the latest version of Mail [most of the folders should be recognized correctly most of the time](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/192).

### Store copy of sent mail in Sent folder

Even though sending emails worked in elementary Mail, it did not always store a copy of the sent mail in the `Sent` folder. That has been fixed in the latest version of elementary Mail and you can expect all sent mails to be stored in the Sent folder for any mail provider. Please note: This wasn't an issue for Office 365 or Gmail users, because these providers copy the sent mail to the `Sent` folder automatically by themselves.

### Handle reply subject

elementary Mail now [correctly displays the subject field](https://github.com/elementary/mail/pull/602) whenever you forward or reply to an email. In addition Mail does now [handle `Re:` subject prefixes correctly](https://github.com/elementary/mail/pull/603) as well whenever you hit the reply button on a received message.

### Save draft

Up until now, the new elementary Mail was not capable of saving a draft. That said, every now and then mails got lost because they were not sent straight away. In the latest version of elementary Mail its quite hard to loose a draft: It is [automatically saved](https://github.com/elementary/mail/pull/599) whenever you leave the compositor ;)

### Edit draft

Saved drafts are not that useful, if they can't be edited. That's exactly what [Pull Request #626](https://github.com/elementary/mail/pull/626) is going to fix. Its not quite done yet, but its nearly there!

### Online Accounts: Verify credentials

And one more thing: The mail account setup in `System Settings > Online Accounts` does now [verify your IMAP/SMTP credentials before they got saved](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/189). Once the setup is sucessfull, you can be sure the mail account actually works in elementary Mail. This fixes a bunch of issues where users did not see any mails - even though the Online Accounts setup wrongly indicated it was sucessful.