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

![New functionality in elementary Mail: Refresh and Filter](../.gitbook/assets/elementary-mail-refresh-and-filter.png)

I dedicated [again](2021-07-25-a-month-dedicated-to-elementary-mail) quite some time to elementary Mail this month - which resulted in a bunch of improvements: Mail now sends a notification to inform you about new messages \([\#679](https://github.com/elementary/mail/pull/679)\) and in case you feel like there is a message missing in your inbox, you are now able to manually refresh the currently selected folder \([\#680](https://github.com/elementary/mail/pull/680)\). Also the user interface feels much smoother when you are now searching for messages \([\#676](https://github.com/elementary/mail/pull/676)\) and on top of that, you are now even able to filter already read or un-starred conversations from the list \([\#678](https://github.com/elementary/mail/pull/678)\)[!](https://github.com/elementary/mail/pull/678]%29!) Last but not least, some bug fixes also made their way into the latest version of Mail: It now avoids to store messages twice in the "Sent" folder for users of outlook.com \([\#702](https://github.com/elementary/mail/pull/702)\) and it also automatically selects the next message after you delete the current one - which lets you delete at light speed \([\#660](https://github.com/elementary/mail/pull/660)[\)!](https://github.com/elementary/mail/pull/660%29!)

|  |  |
| :--- | :--- |


{% hint style="info" %}
If you like my contributions, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Tasks

![elementary Tasks: Drag task to another list](../.gitbook/assets/elementary-tasks-drag-and-drop.png)

In the near future it will be possible to drag and drop tasks to other lists \([\#296](https://github.com/elementary/tasks/pull/296)\). Please note, this still needs to go through review by the elementary team, but for me this addition is huge because the lack of it was the main reason why Tasks was not _yet_ ready for me - so I'm quite excited about this one! In addition to this drag and drop feature, I also fixed the following two bugs: First, by default Tasks now only loads non-completed tasks, which solves an issue where users experienced performance issues \([\#295](https://github.com/elementary/tasks/pull/295)\). Second, Tasks now correctly places the cursor upon focus of the task description field \([\#293](https://github.com/elementary/tasks/pull/293)\) - this will come in especially handy once [HyperTextView](https://github.com/elementary/granite/pull/507) is released into the wild.

## Online Accounts

I changed the way how Online Accounts discovers calendars and task lists, which solved issues with task list managing for CalDAV backends \([\#227](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/227)\). Additionally, Online Accounts now also stores the refresh interval for IMAP accounts \([\#222](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/222)\)- this allows us to make this value configurable in the future.

## Calendar

Since I was already tinkering with notifications this month, I fixed the missing icon bug for notifications in Calendar too \([\#702](https://github.com/elementary/calendar/pull/702)\).

