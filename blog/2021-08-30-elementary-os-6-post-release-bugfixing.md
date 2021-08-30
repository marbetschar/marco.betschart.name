---
description: >-
  I dedicated this month to squash as many bugs as possible in the all new
  elementary OS 6 Odin.
---

# elementary OS 6: Post Release Bugfixing

{% hint style="danger" %}
This is a draft and will most likely be changed.
{% endhint %}

_August 2021_

It's available: elementary OS 6 Odin was released earlier this month! Please see [this elementary blog post](https://blog.elementary.io/elementary-os-6-odin-released/) for a complete overview on what's new.

![elementary OS 6 Odin](../.gitbook/assets/elementary-os-6-odin.png)

New software always contains bugs which slipped through. That's why I dedicated this month to squash as many bugs as possible in the all new elementary OS 6 Odin.

{% hint style="warning" %}
**Please note:** Not all of the fixes described below are already released. Some are still undergoing testings and reviews. So it might take a little more time until those are available to you.
{% endhint %}

## Mail

### Some mails did not load  \([\#655](https://github.com/elementary/mail/pull/655)\)

As you're maybe aware, calculating heights in the web is not an easy task. And we figured, a wrongly calculated height was exactly the reason why some mails were not rendered correctly. Now, the height calculation is fixed and all mails render as expected. 🤞

### Deleting mails sometimes doesn't work \([\#656](https://github.com/elementary/mail/pull/656)\)

Simply put: This was a timeout issue which is now fixed.

### Automatically select next conversation after delete \([\#660](https://github.com/elementary/mail/pull/660)\)

This little improvement automatically selects the next conversation in the list whenever the current one is deleted or archived. This way you can simply delete or archive one conversation after another, without tediously selecting each message by yourself.

### Sender was not always correct \([\#634](https://github.com/elementary/mail/pull/634)\)

If you configured multiple mail accounts, elementary Mail sometimes used the wrong account to send mails from. I fixed this wrong behavior and also made sure you can see the `From:` input field while composing a message. This way you can be 100% sure, your mail is sent from the correct account - and even switch to another one if you like.

## Tasks

### Password not found

Some users claimed they weren't able to access task lists after the account setup. Turned out we ran into a sandbox issue with Flatpak. Solving this "the right way" needs [some more serious engineering effort](https://github.com/elementary/switchboard-plug-onlineaccounts/issues/209), therefore we are shipping Tasks as Debian package again - which mitigates the issue for now.

### Avoid accidentally deleting a list \([\#279](https://github.com/elementary/tasks/pull/279)\)

Because the shortcut chosen to delete a task list was also triggered while editing a task item, it may lead to data loss. Now the shortcut is deactivated during task editing.

### Account header in sidebar is sometimes shown multiple times \([\#287](https://github.com/elementary/tasks/pull/287)\)

An issue while sorting task lists caused the account name in the sidebar to be shown multiple times under certain circumstances. This is fixed now.

### Can't remove task description \([286](https://github.com/elementary/tasks/pull/286)\)

Whenever a task description was completely removed, the user interface did not reflect this state properly.

## System Settings: Online Accounts

### Auto detect auth mechanism \([\#211](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/211)\)

Some users weren't able to add their mail accounts in `System Settings > Online Accounts`, because of the authentication method used. Online Accounts is now capable to probe for authentication methods supported by the server and chooses the right one automatically.

### Edit Mail and CalDAV account \([\#208](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/208), \#[216](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/216)\)

It is now possible to edit an existing mail or calendar account in `System Settings > Online Accounts`.

### Ignore Calendar Subscriptions \([\#218](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/218)\)

Synchronizing subscribed calendars threw an error under certain circumstances. Because there is no way for us to know the correct credentials for such subscriptions, we are simply ignoring those for now. In case you use calendar subscriptions, you need to add them in the corresponding app directly.

|  |  |
| :--- | :--- |


{% hint style="info" %}
If you like my contributions, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## System Settings: Notifications

### Bypass Do Not Disturb \([\#84](https://github.com/elementary/switchboard-plug-notifications/pull/84)\)

And one more thing: I also worked on a feature which allows you to configure specific apps to bypass "Do Not Disturb". This way you'll be able to fully focus on the task at hand by turning off all notifications - except those few you really rely on, such as meeting notifications or a [timer](https://appcenter.elementary.io/com.github.marbetschar.time-limit/).

