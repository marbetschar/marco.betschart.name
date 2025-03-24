---
tags:
  - linux-desktop
  - elementary
  - ux
description: >-
  Things I miss on elementary OS to make this already amazing Linux Desktop an
  even better and more productive experience for me.
---

# Missing Features & Workarounds

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## 🌍 Online Accounts

### OAuth Support (Modern Authentication)

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/portals/issues/19) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

It would be great to have Online Accounts support mordern authentication protocols such as OAuth. This would make setting up Office 365 corporate or Google Mail accounts both easier and more secure.

**Workaround:** Install Evolution and Evolution EWS from deb (`sudo apt install evolution evolution-ews`) and configure such accounts there:

1. Start Evolution
2. Start the New Mail Account Wizard: Click `File > New > Mail Account`
3. Enter your **Email Address** and **uncheck** `Look up mail server details…`, click `Next`
4. Select **Server Type**: `Exchange Web Services`

* Set **Host URL**: `https://outlook.office365.com/EWS/Exchange.asmx`
* Click **Check for Supported Types** - this should select `OAuth2 (Office 365)`
* **Check** `Override Office 365 OAuth2 settings`
* Open the [**Help…**](https://wiki.gnome.org/Apps/Evolution/EWS/OAuth2) link and follow the instructions provided there.

## 📆️ Calendar

### Weekly View

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/calendar/issues/500) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

Beeing able to plan events using a weekly grid which shows 7 full days instead of one square per day in a month.

**Workaround:** Use another app which provides a weekly view.

## 📂 Files

### Clone repository from clipboard

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: Won't Fix](https://img.shields.io/badge/status-wontfix-red)](https://github.com/elementary/files/pull/1310) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

Beeing able to clone a repository from an url stored in clipboard without leaving elementary Files. The current solution enables this behaviour by adding a context menu option if the content of the clipboard contains a valid Git URL.

**Workaround:** Execute `git clone ...url...` from Terminal.

## ✉️ Mail

### Drag message to another folder

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/mail/issues/633) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

It should be possible to drag a message to another folder.

**Workaround:** Login into your webmail and move the message there.

### Filter & Search for flagged emails

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: In Progress](https://img.shields.io/badge/status-in_progress-green)](https://github.com/elementary/mail/pull/678) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

It should be possible to search and filter only through flagged emails. Ideally through multiple mail accounts at the same time.

**Workaround:** None.

### Save inline image to disk

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/mail/issues/447) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

I don't seem to be able to save an inline image in Mail to the file system. That's a bit unfortunate, since these days the default behaviour for the macOS Mail App seems to be to send images using the builtin share function like this: As inline content - not as regular attachment.

**Workaround:** Go to your webmail and download the image from there.

## 🧙‍♂️️ Window Manager (Gala)

### Glimpse at unlocked Desktop after resume

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/gala/issues/988) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

When my laptop suspends the screen goes dark, but when I wake it up again I can get a quick glimpse at the unlocked Desktop before the login form is shown.

### Picture-in-Picture: hard to resize without moving away from bottom/right edges

![Last Update: 2021-12-26](https://img.shields.io/badge/last%20update-2021--12--26-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/gala/issues/1116) ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20J%C3%B3lnir-007aff)

Its hard to resize the Picture-in-Picture window, if it is placed in the lower right corner of the screen. That's due to the resize button beeing in the bottom right corner - therefore it is not possible to make the Picture-in-Picture window bigger without beeing moved away from the corner first.
