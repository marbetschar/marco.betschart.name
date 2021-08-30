---
description: >-
  I dedicated this month to squash bugs in newly released elementary OS 6 Odin.
---

# elementary OS 6: Post Release Bugfixing

_August 2021_

It's available: elementary OS 6 Odin was released earlier this month! See [the elementary blog](https://blog.elementary.io/elementary-os-6-odin-released/) for a complete overview on what's new.

![elementary OS 6 Odin](../.gitbook/assets/io.elementary.mail.png)

Whenever new software is released, there are some edge cases and bugs which slipped through. That's why I dedicated this month
to squash bugs in elementary OS 6 Odin - as well as adding a few convenience features. Always with the goal to improve the overall
productivity of office tasks in elementary OS:

## Mail

### Some mails did not load

As you're maybe aware, calculating heights in the web is not always an easy task - and a wrongly calculated height was exactly the reason, why some mails did not render correctly in elementary Mail. Now, the height calculation is fixed and all mails show up as they should ([#655](https://github.com/elementary/mail/pull/655)).

### Deleting mails sometimes doesn't work

Simply put: This was a timeout issue which is now fixed ([#656](https://github.com/elementary/mail/pull/656)).

### Automatically select next message after delete

This little improvement automatically selects the next message in the list whenever the current one is deleted or archived. This way you can simply delete or archive one message after another, without tediously selecting each message by yourself ([#660](https://github.com/elementary/mail/pull/660)).

### Sender was not always correct

If you configured multiple mail accounts, elementary Mail sometimes used the wrong account to send mails from. I fixed this wrong behaviour and also made sure
you can see the `From:` input field while composing the message. This way you can be sure, your mail is sent from the correct account - and even switch to another
one if you want to ([#634](https://github.com/elementary/mail/pull/634)).

|  |  |
| :--- | :--- |

{% hint style="info" %}
If you like my contributions, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Tasks

### Password not found

Some users claimed they were not able to access task lists after account configuration in `System Settings > Online Accounts`. Turned out
we ran into sandboxing issues with Flatpak. Because solving this properly needs [some more serious engineering effort](https://github.com/elementary/switchboard-plug-onlineaccounts/issues/209), we are shipping Tasks as Debian package for now. This solves the issue these user's are facing.

###  Avoid accidentally deleting a list

Because the shortcut chosen to delete a task list was also triggered while editing a task item, it unfortunately lead to data loss in some cases. I deactivated the shortcut during task editing now, so this is no longer the case ([#279](https://github.com/elementary/tasks/pull/279)).

### Account header in sidebar is sometimes shown multiple times

An issue while sorting the task lists caused the account name in the sidebar to be shown multiple times under certain circumstances. This is fixed now ([#287](https://github.com/elementary/tasks/pull/287)).

### Can't remove task description

Whenever a task description was completely removed, the UI did not reflect this state correctly ([286](https://github.com/elementary/tasks/pull/286)).

## System Settings

### Online Accounts

### Auto detect auth mechanism

Some users weren't able to add their mail accounts in `System Settings > Online Accounts`, because of the authentication method used under the hood.
Online Accounts is capable to probe for authentication methods supported by the server and chooses the right one automatically ([#211](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/211)).

### Edit Mail and CalDAV account

It is now possible to edit an existing [mail](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/208) as well as [calendar](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/216) account in `System Settings > Online Accounts` ([#208]).

### Ignore Calendar Subscriptions

Synchronizing subscribed calendars threw an error under certain circumstances. Because there is no way for us to know the correct credentials for such calendar subscriptions, we are simply ignoring any subscriptions for now ([#218](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/218)). In case you use subscriptions, you need to add those in the corresponding app.

### Notifications

And there is one last thing: I also worked on a [feature allowing user specific apps to bypass Do Not Disturb](https://github.com/elementary/switchboard-plug-notifications/pull/84). Once this is released, you'll be able to fully focus on the task at hand by turning off all notifications - except those few you really rely on.