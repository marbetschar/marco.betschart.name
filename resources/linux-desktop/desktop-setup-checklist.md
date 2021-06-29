---
description: My personal checklist for setting up a fresh elementary OS installation.
---

# Setup Checklist

## Desktop

* [ ] Start `Files` and click `Keep in Dock`
* [ ] Set `⌘+E` in `System Settings > Keyboard > Shortcuts > Applications > Home Folder`
* [ ] Set correct `Format and Temperature` in `System Settings > Language & Region` \(you may need to complete language support installation before\)
* [ ] Adjust `System Settings > Date & Time`:
  * [ ] Disable `Based on location`
  * [ ] Select correct Time zone
  * [ ] Enable `Show week numbers`
* [ ] Increase pointer speed one mark in `System Settings > Mouse & Touchpad > Touchpad`
* [ ] Log out and back in again

## Firefox

* [ ] Install from AppCenter
* [ ] Start Firefox and login to Firefox Account
* [ ] Select `DuckDuckGo` in `Firefox > Settings > Search > Default Search Engine`
* [ ] Select Firefox in `System Settings > Applications > Web Browser`

## Nextcloud Client

* [ ] [Install as documented](install-nextcloud-client.md)
* [ ] Start Nextcloud desktop sync client and login to Nextcloud account
* [ ] Make sure Nextcloud is listed to autostart in `System Settings > Applications > Startup`

## AppImageLauncher

* [ ] [Install as documented](https://github.com/TheAssassin/AppImageLauncher/wiki/Install-on-Ubuntu-or-Debian)

## Paymo

* [ ] [Download the Paymo Desktop App from the Website](https://www.paymoapp.com/downloads-and-integrations/)
* [ ] Open the downloaded AppImage in Files \(double click\)
* [ ] Confirm `~/Applications` as integration target destination directory
* [ ] Click `Integrate and run`
* [ ] Login to Paymo Account

## Online Accounts

Setup Online Accounts in `System Settings > Online Accounts`:

**Private**

* [ ] Calendar and Tasks stored in Nextcloud \(needs application specific password\)
* [ ] Mail

|  | Server | Port | Encryption |
| :--- | :---: | :---: | :---: |
| _Incoming Mail \(IMAP\)_ | imap.yandex.com | 993 | SSL |
| _Outgoing Mail \(SMTP\)_ | smtp.yandex.com | 465 | SSL |

[_yandex.com/support/mail/mail-clients.html_](https://yandex.com/support/mail/mail-clients.html)

**Work and Studies**

* [ ] Mail

|  | Server | Port | Encryption |
| :--- | :---: | :---: | :---: |
| _Incoming Mail \(IMAP\)_ | outlook.office365.com | 993 | SSL/TLS |
| _Outgoing Mail \(SMTP\)_ | outlook.office365.com | 587 | STARTTLS |

[_support.microsoft.com/en-us/office/pop-imap-and-stmp-settings-8361e398-8af4-4e97-b147-6c6c4ac95353_](https://support.microsoft.com/en-us/office/pop-imap-and-stmp-settings-8361e398-8af4-4e97-b147-6c6c4ac95353)



