---
description: >-
  Things I miss on elementary OS to make this already amazing Linux Desktop an
  even better and more productive experience for me.
tags:
  - linux-desktop
  - elementary
  - ux
---

# Missing Features & Workarounds

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## 📂 Files

### Clone repository from clipboard

![Last Update: 2021-02-17](https://img.shields.io/badge/last%20update-2021--02--17-lightgrey?style=social) [![Status: In Progress](https://img.shields.io/badge/status-in_progress-green)](https://github.com/elementary/files/pull/1310) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

Beeing able to clone a repository from an url stored in clipboard without leaving elementary Files. The current solution enables this behaviour by adding a context menu option if the content of the clipboard contains a valid Git URL.

**Workaround:** Execute `git clone ...url...` from Terminal.

### ~~Extract / Compress from context menu~~

![Last Update: 2021-03-08](https://img.shields.io/badge/last%20update-2021--03--08-lightgrey?style=social) [![Status: Fixed](https://img.shields.io/badge/status-fixed-green)](https://github.com/elementary/os-patches/issues/136) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

~~Beeing able to quickly zip and unzip files by simply doing a right click. This was possible on Hera.~~

~~**Workaround:** Execute the following command in your Terminal to install the missing file contractor:~~

```bash
sudo apt install io.elementary.contractor.file-roller
```

## ✉️ Mail 2.0

### ~~Ability to archive a message~~

![Last Update: 2021-05-06](https://img.shields.io/badge/last%20update-2021--05--06-lightgrey?style=social) [![Status: Fixed](https://img.shields.io/badge/status-fixed-green)](https://github.com/elementary/os-patches/issues/136) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

~~Currently it is not possible to archive a message.~~

~~**Workaround:** Archive your message via other means \(Webmail, iOS, ...\)~~

### Grouped Folders

![Last Update: 2021-05-06](https://img.shields.io/badge/last%20update-2021--05--06-lightgrey?style=social) [![Status: In Progress](https://img.shields.io/badge/status-in_progress-green)](https://github.com/elementary/files/pull/1310) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

It would be convenient to add grouped folders - at least for well known folder names. That is: Inbox, Archive, Drafts, Sent. I would expect these folders to be shown at the very top, containing the messages from all configured email accounts. This way we can get one single Inbox folder, showing an overview for all received messages, one single Archive folder showing all archived messages, ... etc.

**Workaround:** None.

### Filter & Search for flagged emails

![Last Update: 2021-02-17](https://img.shields.io/badge/last%20update-2021--02--17-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/mail/issues/236) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

It should be possible to search and filter only through flagged emails. Ideally through multiple mail accounts at the same time.

**Workaround:** None.

### Save inline image to disk

![Last Update: 2021-02-17](https://img.shields.io/badge/last%20update-2021--02--17-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/mail/issues/447) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

I don't seem to be able to save an inline image in Mail to the file system. That's a bit unfortunate, since these days the default behaviour for the macOS Mail App seems to be to send images using the builtin share function like this: As inline content - not as regular attachment.

**Workaround:** Go to your webmail and download the image from there.

## ~~☁️ Online Accounts~~

### ~~Manage Mail Accounts~~

![Last Update: 2021-06-06](https://img.shields.io/badge/last%20update-2021--06--06-lightgrey?style=social) [![Status: Fixed](https://img.shields.io/badge/status-fixed-green)](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/184) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

~~Managing mail accounts in system settings' Online Accounts.~~

~~**Workaround**~~

~~Install~~ [~~Evolution~~](https://wiki.gnome.org/Apps/Evolution/) ~~and configure the mail accounts there. You'll need the providers IMAP and SMTP settings:~~

~~_**Office 365**_~~

|  | Server | Port | Encryption |
| :--- | :---: | :---: | :---: |
| **Incoming Mail \(IMAP\)** | outlook.office365.com | 993 | SSL/TLS |
| **Outgoing Mail \(SMTP\)** | outlook.office365.com | 587 | STARTTLS |

[~~_support.microsoft.com/en-us/office/pop-imap-and-stmp-settings-8361e398-8af4-4e97-b147-6c6c4ac95353_~~](https://support.microsoft.com/en-us/office/pop-imap-and-stmp-settings-8361e398-8af4-4e97-b147-6c6c4ac95353)

~~_**Yandex**_~~

|  | Server | Port | Encryption |
| :--- | :---: | :---: | :---: |
| **Incoming Mail \(IMAP\)** | imap.yandex.com | 993 | SSL |
| **Outgoing Mail \(SMTP\)** | smtp.yandex.com | 465 | SSL |

[~~_yandex.com/support/mail/mail-clients.html_~~](https://yandex.com/support/mail/mail-clients.html)

### ~~Nextcloud: Calendar and Task Synchronization~~

![Last Update: 2021-06-06](https://img.shields.io/badge/last%20update-2021--06--06-lightgrey?style=social) [![Status: Fixed](https://img.shields.io/badge/status-fixed-green)](https://github.com/elementary/switchboard-plug-onlineaccounts/pull/159) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

~~Managing Contact, Calendar and Task synchronisation for within Online Accounts.~~

~~**Workaround**~~

~~Install~~ [~~Evolution~~](https://wiki.gnome.org/Apps/Evolution/) ~~and configure a "Collection Account" there.~~

## 📦 Package Manager \(apt\)

### add-apt-repository fails with Error: could not find a distribution template for Elementary/next

![Last Update: 2021-02-17](https://img.shields.io/badge/last%20update-2021--02--17-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/os-patches/issues/136) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

Executing `add-apt-repository` fails with the following error:

```bash
Traceback (most recent call last): File "/usr/bin/add-apt-repository", line 108,
in sp = SoftwareProperties(options=options) File "/usr/lib/python3/dist-packages/softwareproperties/SoftwareProperties.py", line 118,
in init self.reload_sourceslist() File "/usr/lib/python3/dist-packages/softwareproperties/SoftwareProperties.py", line 613,
in reload_sourceslist self.distro.get_sources(self.sourceslist)
File "/usr/lib/python3/dist-packages/aptsources/distro.py", line 91,
in get_sources raise NoDistroTemplateException( aptsources.distro.NoDistroTemplateException:
Error: could not find a distribution template for Elementary/odin
```

**Workaround:** [Follow the documented solution here](fix-error-distribution-template-for-elementary-odin.md).

## 🧙‍♂️️ Window Manager \(Gala\)

### Glimpse at unlocked Desktop after resume

![Last Update: 2021-02-17](https://img.shields.io/badge/last%20update-2021--02--17-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/gala/issues/988) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

When my laptop suspends the screen goes dark, but when I wake it up again I can get a quick glimpse at the unlocked Desktop before the login form is shown.

### Picture-in-Picture: hard to resize without moving away from bottom/right edges

![Last Update: 2021-05-06](https://img.shields.io/badge/last%20update-2021--05--06-lightgrey?style=social) [![Status: Confirmed](https://img.shields.io/badge/status-confirmed-orange)](https://github.com/elementary/gala/issues/1116) ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)

Its hard to resize the Picture-in-Picture window, if it is placed in the lower right corner of the screen. That's due to the resize button beeing in the bottom right corner - therefore it is not possible to make the Picture-in-Picture window bigger without beeing moved away from the corner first.

