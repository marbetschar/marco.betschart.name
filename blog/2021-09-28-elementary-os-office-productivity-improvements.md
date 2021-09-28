---
description: Another month and even more office productivity improvements!
---

# elementary OS: Office Productivity Improvements

_September 2021_

See below to see what you can expect from my work on elementary OS during this September.

{% hint style="warning" %}
**Please note:** Not all of the features described below are already released. Some are still undergoing testings and reviews. So it might take a little more time until those are available to you.
{% endhint %}

## Mail

[Once again](https://www.marco.betschart.name/blog/2021-07-25-a-month-dedicated-to-elementary-mail), I dedicated quite some time to elementary Mail. The result are a bunch of improvements:

Mail now sends a notification to inform you about new messages \([\#679](https://github.com/elementary/mail/pull/679)\) and in case you feel like there is a message missing, you are now able to manually refresh the currently selected folder \([\#680](https://github.com/elementary/mail/pull/680)\).

![Mail notifies you about new messages](../.gitbook/assets/elementary-mail-notifications.png)

Also the user interface feels much smoother when you are searching for messages \([\#676](https://github.com/elementary/mail/pull/676)\) and on top of that, you are now even able to hide already read or un-starred conversations from the list \([\#678](https://github.com/elementary/mail/pull/678)\)[!](https://github.com/elementary/mail/pull/678]%29!)

![New functionality in elementary Mail: Refresh and Filter](../.gitbook/assets/elementary-mail-refresh-and-filter.png)

Last but not least, the following two bug fixes also found their way into the latest version of Mail: It now avoids to store messages twice in the "Sent" folder for users of outlook.com \([\#702](https://github.com/elementary/mail/pull/702)\) and it also automatically selects the next message after you delete the current one - which lets you delete at light speed \([\#660](https://github.com/elementary/mail/pull/660)[\)!](https://github.com/elementary/mail/pull/660%29!)

|  |  |
| :--- | :--- |


{% hint style="info" %}
If you like my contributions, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Tasks

![elementary Tasks: Drag task to another list](../.gitbook/assets/elementary-tasks-drag-and-drop.png)

In the near future it will be possible to drag and drop tasks to another list \([\#296](https://github.com/elementary/tasks/pull/296)\). For me, this addition is huge! The lack of it was the main reason for me, why Tasks was _not quite usable_ - so I'm very excited about this one!

In addition to this new drag and drop feature, I also fixed two bugs:

First, Tasks now only loads non-completed tasks by default. This solves some performance issues \([\#295](https://github.com/elementary/tasks/pull/295)\).

Second, the cursor of the task description field is not correctly placed \([\#293](https://github.com/elementary/tasks/pull/293)\) - this improves usability and paves the way for a future integration of [HyperTextView](https://github.com/elementary/granite/pull/507) once it is released.

## Online Accounts

I refactored the calendars and task list discovery in Online Accounts, which solves issues with task list management for CalDAV backends \([\#227](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/227)\). Additionally, Online Accounts now stores a refresh interval for IMAP accounts \([\#222](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/222)\) - this enables us to make this value configurable in the future.

## Calendar

As I was tinkering with notifications already, I fixed the missing icon bug for notifications in Calendar as well \([\#702](https://github.com/elementary/calendar/pull/702)\).

