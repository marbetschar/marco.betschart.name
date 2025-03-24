---
description: My personal checklist for setting up a fresh Arch Linux installation.
---

# Setup Checklist

## GNOME Settings

* [ ] Enable `Mouse & Touchpad > Tap to Click`
* [ ] Navigate to `Keyboard > View and Customize Shortcuts`:
  * [ ] Set `Launchers > Home folder` to `Super + E`
  * [ ] Set `Navigation > Switch Windows` to `Alt + Tab`
  * [ ] Create a shortcut in `Custom Shortcuts`:
    * Name: `Console`
    * Command: `kgx --tab`
    * Shortcut: `Super + T`

## GNOME Apps

Install Calendar, Evolution and Endeavour:

```shell
sudo pacman -S gnome-calendar gnome-contacts endeavour evolution evolution-ews
```

## GNOME with X11

### Mouse Gestures

**PLEASE NOTE:** At the time of this writing (2023-01-29), screen sharing is broken in MS Teams under Wayland. In order to use this feature, make sure you are logging into an X11 session. Unfortunately under X11 the mouse gestures don't work out of the box - but this is fixable:

```shell
yay touchegg gnome-shell-extension-x11gestures
sudo systemctl enable touchegg.service
sudo systemctl start touchegg

# Enable the X11 Gesture Extension:
gnome-extensions enable x11gestures@joseexposito.github.io
```

For details see: https://bbs.archlinux.org/viewtopic.php?id=265360

### Fix Flickering in Screen Sharing

If you experiencing flickering while sharing your screen in for example Microsoft Teams or Zoom, make sure to use the modesetting driver in X11. To do so, simply remove `xf86-video-intel`, and possibly `/etc/X11/xorg.conf.d/20-intel.conf` - then reboot:

```shell
sudo pacman -Rs xf86-video-intel
```

For details see: https://bbs.archlinux.org/viewtopic.php?id=218021

## Flatpak

Install [as documented for EndeavourOS](https://www.flatpak.org/setup/EndeavourOS):

```shell
sudo pacman -Syu
sudo pacman -S flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

Then restart your system.

## Nextcloud Client

Install [Nextcloud Client from Flathub](https://flathub.org/apps/details/com.nextcloud.desktopclient.nextcloud):

```shell
flatpak install flathub com.nextcloud.desktopclient.nextcloud
```

Then start the client and login to your Nextcloud to start the synchronization process. To enable Autostart, open GNOME Tweaks, go to `Startup Applications` and add Nextcloud Desktop there. This literally just creates the `~/.config/autostart/com.nextcloud.desktopclient.nextcloud.desktop` file.

## Git

Execute the following commands in the Terminal:

```shell
git config --global user.name "Your Name"
git config --global user.email "your.name@domain.tld"
ssh-keygen -t ed25519 -C "your.name@domain.tld"
cat .ssh/id_ed25519.pub
```

Add the SSH Public Key to the following portals:

* [ ] [GitHub.com](https://github.com/settings/keys)
* [ ] [freedesktop.org GitLab](https://gitlab.freedesktop.org/-/profile/keys)
* [ ] [GitLab.com](https://gitlab.com/-/profile/keys)
* [ ] [GNOME GitLab](https://gitlab.gnome.org/-/profile/keys)

## VSCodium

Install VSCodium from AUR by executing the following command in the Terminal:

```shell
yay vscodium-bin
```

Verify whether `Super + E` still opens Nautilus in your home folder - or you end up in VSCodium now. If VSCodium is started, this is [due to a bug](https://forum.manjaro.org/t/keyboard-mapping-not-sticking-super-e-opens-vscodium/101462/3) which causes the default file ordering to be messed up:

```shell
$ cat /usr/share/applications/mimeinfo.cache | grep inode/directory
inode/directory=codium.desktop;org.gnome.Nautilus.desktop;
```

To fix this, create a new file in `~/.config/mimeapps.list` and fix the ordering there by adding the following content:

```
[Default Applications]
inode/directory=org.gnome.Nautilus.desktop;
```

Then Logout and Login again to restart your GNOME Session and `Super + E` should now open Nautilus again.

## Paymo Widget

Install the Paymo Widget from AUR by executing the following command in the Terminal:

```shell
yay paymo-widget
```

## Signal Desktop

Install the [Signal Desktop application from Flathub](https://flathub.org/apps/details/org.signal.Signal):

```shell
flatpak install flathub org.signal.Signal
```

## Online Accounts

Setup Online Accounts in `GNOME Settings > Online Accounts`:

**Private**

* [ ] `Nextcloud` for Calendar and Contacts (needs application specific password)
* [ ] `IMAP and SMTP` for Mail

|                        |     Server     | Port | Encryption |
| ---------------------- | :------------: | :--: | :--------: |
| _Incoming Mail (IMAP)_ | mail.gandi.net |  993 |     SSL    |
| _Outgoing Mail (SMTP)_ | mail.gandi.net |  587 |  STARTTLS  |

[_docs.gandi.net/en/gandimail/standard\_email\_settings/_](https://docs.gandi.net/en/gandimail/standard_email_settings/)

**Study & Work**

* [ ] Calendar and Tasks
* [ ] Mail

Install Evolution and Evolution EWS (`sudo pacman -S evolution evolution-ews`) and configure these accounts there:

1. Start Evolution
2. Start the New Mail Account Wizard: Click `File > New > Mail Account`
3. Enter your **Email Address** and **uncheck** `Look up mail server details…`, click `Next`
4. Select **Server Type**: `Exchange Web Services`

* Set **Host URL**: `https://outlook.office365.com/EWS/Exchange.asmx`
* Click **Check for Supported Types** - this should select `OAuth2 (Office 365)`
* **Check** `Override Office 365 OAuth2 settings`
* Enter the **Tenant ID** of your account (copy the `tid` query parameter value from your account url in Outlook Web Access)
* Open the [**Help…**](https://wiki.gnome.org/Apps/Evolution/EWS/OAuth2) link and follow the instructions provided there.

In case you run into any troubles due to the Evolution application ID not beeing authorized by your Office 365 administrator, use the last Evolution application ID with the Redirect URI set to `urn:ietf:wg:oauth:2.0:oob` [as descrdibed in the GNOME Wiki](https://wiki.gnome.org/Apps/Evolution/EWS/OAuth2).

**Unified Inbox in Evolution**

To have a grouped inbox view in Evolution I am going to use the `Search Folders` feature. Go to `Edit > Preferences` and enable `Search Folders`. Then drag it the top. Then create a new Search Folder in `Edit > Search Folders > Add` with the following settings:

* Rule name: `Inbox`
* Find items which match: `any of the following conditions`
* Include threads: `None`
* `Message Location`: `is`: `Your Account/Inbox`
  * Add as many `Message Location` conditions as you have accounts and inboxes
* **Check** Automatically update on any source folder change
* Select `All active remote folders`
* Then click **Ok**

Repeat the above steps for any Unified Folder you want to have (e.g. for `Archive`).

## Microsoft Teams

Install the [Microsoft Teams application from Flathub](https://flathub.org/apps/details/com.microsoft.Teams):

```shell
flatpak install flathub com.microsoft.Teams
```

## Cryptomator

Install the [Cryptomator application from Flathub](https://flathub.org/apps/details/org.cryptomator.Cryptomator):

```shell
flatpak install flathub org.cryptomator.Cryptomator
```

## Espanso

Install [Espanso from AUR](https://aur.archlinux.org/packages/espanso-bin):

```shell
yay espanso-bin

# Autostart Espanso:
espanso service register
# Start Espanso now:
espanso service start
```

## Skype

Install the [Skype application from Flathub](https://flathub.org/apps/details/com.skype.Client):

```shell
flatpak install flathub com.skype.Client
```

## Zettelkasten

Install [Zettlr](https://flathub.org/apps/details/com.zettlr.Zettlr), [Zotero](https://flathub.org/apps/details/org.zotero.Zotero) and [Flatseal](https://flathub.org/apps/details/com.github.tchx84.Flatseal) from Flathub:

```shell
flatpak install flathub com.zettlr.Zettlr flathub org.zotero.Zotero flathub com.github.tchx84.Flatseal
```

* Open `Flatseal`, select `Zettlr` and enable `filesystem=home` permission
* Start Zettlr and in `File > Open Workspace ...` select `~/Nextcloud/Notes`
* Last but not least, start `Zotero` and [configure it as documented](../knowledge-management/howto-setup-zotero.md)

## PDF Studio Pro

* [ ] [Go to the Qopppa Software download page](https://kbpdfstudio.qoppa.com/download-previous-versions/)
* [ ] Select PDF Studio 2022
* [ ] Enter the License Key stored at `Resources/Akten` to download PDF Studio 2022
* [ ] Start the installer from Terminal: `sh ~/Downloads/PDFStudio_*.sh`
* [ ] Activate the software using the License Key stored at `Resources/Akten`
* [ ] Go to `File > Preferences > Display` and select:
  * [ ] `THeme: Dark`
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

## eGPU with X11

First, reboot with your eGPU attached. Then install the correct drivers for your graphic card:

```shell
sudo pacman -S xf86-video-amdgpu vulkan-radeon
```

Second, install and setup the [egpu-switcher](https://github.com/hertg/egpu-switcher) from AUR:

```shell
# Install:
$ yay -S egpu-switcher-bin

# Configure:
$ sudo egpu-switcher config

Found 2 possible GPU(s)...

1: 	Intel Corporation TigerLake-LP GT2 [Iris Xe Graphics] (i915)
2: 	Advanced Micro Devices, Inc. [AMD/ATI] Navi 23 [Radeon RX 6600/6600 XT/6600M] (amdgpu)

Which one is your external GPU? [1-2]: 2

[ok] Your selection was saved to the config file

# Enable
$ sudo egpu-switcher enable
```

At this stage you are fully set. Reboot your system once again and keep the eGPU attached. You should now be able to login and the eGPU is used by default.

To verify, go to `GNOME System Settings > About` - there it should display your eGPU's name.

For more information, check the [External GPU article in the Arch Wiki](https://wiki.archlinux.org/title/External_GPU).

## AppImageLauncher

Install AppImageLauncher from AUR by executing the following command in the Terminal:

```shell
yay appimagelauncher-git
```

## Steam

```shell
sudo pacman -Sy
...
sudo pacman -S steam
...
:: There are 5 providers available for vulkan-driver:
:: Repository extra
   1) amdvlk  2) nvidia-utils  3) vulkan-intel  4) vulkan-radeon  5) vulkan-swrast

Enter a number (default=1): 4
:: There are 4 providers available for lib32-vulkan-driver:
:: Repository multilib
   1) lib32-amdvlk  2) lib32-nvidia-utils  3) lib32-vulkan-intel  4) lib32-vulkan-radeon

Enter a number (default=1): 4
...
```

**PLEASE NOTE:** At the time of this writing (2022-08-26), SteamVR only works (sort of) on X11, not on Wayland.
