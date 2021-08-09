---
description: My personal checklist for setting up a fresh elementary OS installation.
---

# Setup Checklist

## System

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

* [ ] [Install as documented](../../resources/linux-desktop/install-nextcloud-client.md)
* [ ] Start Nextcloud desktop sync client and login to Nextcloud account
* [ ] Make sure Nextcloud is listed to autostart in `System Settings > Applications > Startup`

## Signal Desktop

* [ ] Click `Install` on [Signal's FlatHub.org page](https://flathub.org/apps/details/org.signal.Signal)
* [ ] Choose `Open with Sideload`
* [ ] Select `I understand` and click `Install Anyway`
* [ ] Select `Move *.flatpakref to Trash` and click `Open App`

## AppImageLauncher

* [ ] [Install as documented](https://github.com/TheAssassin/AppImageLauncher/wiki/Install-on-Ubuntu-or-Debian)

## Paymo

* [ ] [Download the Paymo Desktop App from the Website](https://www.paymoapp.com/downloads-and-integrations/)
* [ ] Open the downloaded AppImage in Files \(double click\)
  * [ ] If prompted, confirm `~/Applications` as integration target destination directory
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

## Git

Execute the following commands in the Terminal:

```text
sudo apt install git
git config --global user.name "Your Name"
git config --global user.email "your.name@domain.tld"
ssh-keygen -t rsa
cat ~/.ssh/id_rsa.pub
```

Add the SSH Public Key to the following portals:

* [ ] [GitHub.com](https://github.com/settings/keys)
* [ ] [GitLab.com](https://gitlab.com/-/profile/keys)
* [ ] [GNOME GitLab](https://gitlab.gnome.org/-/profile/keys)
* [ ] Gitea @Work
* [ ] GitHub @Studies

## elementary Development

* [ ] [Install VSCodium with Vala Autocompletion as documented](../../resources/linux-desktop/vscode-setup-vala-autocompletion.md)
* [ ] Install elementary Development Libraries: `sudo apt install elementary-sdk`

## Zettelkasten

* [ ] [Download the \*.deb package from the Zettlr website](https://www.zettlr.com/download)
* [ ] Install with: `sudo apt install ~/Downloads/Zettlr-*.deb`
* [ ] Clone Zettelkasten with Git from Remote using SSH to `~/Zettelkasten`
* [ ] Add `~/Zettelkasten` to Bookmarks in `Files`

## Cryptomator

* [ ] [Download the Cryptomator App from the Website](https://cryptomator.org/downloads/)
* [ ] Open the downloaded AppImage in Files \(double click\)
  * [ ] If prompted, confirm `~/Applications` as integration target destination directory
* [ ] Click `Integrate and run`
* [ ] Add Vaults as needed

## Espanso

* [ ] [Clone Linux User Home Configuration Files as documented](https://github.com/marbetschar/config/)
* [ ] [Install espanso from DEB package as documented](https://espanso.org/install/linux/)

## VPN

* [ ] Work
  * [ ] Configure as documented in Zettelkasten
* [ ] Studies
  * [ ] `sudo apt install network-manager-openconnect-gnome`
  * [ ] Click `+` in `System Settings > Network > VPN`
  * [ ] Select `Cisco AnyConnect or openconnect (OpenConnect)` and click `Create…`
  * [ ] Enter `ras.zhaw.ch` as Gateway

## Printing & Scanning

* [ ] [Setup HP Color Laser Jet Pro MFP M281 fdw as documented](../../resources/linux-desktop/setup-hp-color-laser-jet-pro-mfp-m281-fdw.md)

## Gscan2pdf

* [ ] `sudo apt install gscan2pdf tesseract-ocr-deu tesseract-ocr-eng`
* [ ] Start Gscan2pdf and navigate to `Edit > Preferences > General Options`:
  * [ ] Set Default PDF & DjVu filename to `%Dy%Dm%Dd %Dt %Da.%De`

## PDF Studio Pro

* [ ] [Go to the Qopppa Software download page](https://kbpdfstudio.qoppa.com/download-previous-versions/)
* [ ] Select PDF Studio 2020
* [ ] Enter the License Key stored at `Resources/Akten` to download PDF Studio 2020
* [ ] Start the installer from Terminal: `sh ~/Downloads/PDFStudio_*.sh`
* [ ] Activate the software using the License Key stored at `Resources/Akten`
* [ ] Go to `File > Preferences > Display` and select:
  * [ ] `Look & Feel: Metal`
  * [ ] `Document Resolution: System Setting`
* [ ] Go to `File > Preferences > Application` and **deactivate** `Run in background`
* [ ] Restart the application
* [ ] Go to `File > Preferences > General` and select:
  * [ ] `Units: Centimeters`
  * [ ] `Default Page Size: A4`
* [ ] Go to `File > Preferences > OCR` and:
  * [ ] Click `Download OCR Languages`
  * [ ] Select `English` and `German - Deutsch`
  * [ ] Click `Download`
  * [ ] Set `Primary Language: German - Deutsch`
  * [ ] Check `Enable Secondary Language: English`

