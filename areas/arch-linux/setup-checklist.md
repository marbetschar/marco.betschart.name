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

```text
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

|  | Server | Port | Encryption |
| :--- | :---: | :---: | :---: |
| _Incoming Mail \(IMAP\)_ | mail.gandi.net | 993 | SSL |
| _Outgoing Mail \(SMTP\)_ | mail.gandi.net | 587 | STARTTLS |

[_docs.gandi.net/en/gandimail/standard_email_settings/_](https://docs.gandi.net/en/gandimail/standard_email_settings/)

**Study & Work**

* [ ] Calendar and Tasks
* [ ] Mail

Install Evolution and Evolution EWS (`sudo pacman -S evolution evolution-ews`) and configure these accounts there:

1. Start Evolution
2. Start the New Mail Account Wizard: Click `File > New > Mail Account`
3. Enter your **Email Address** and **uncheck** `Look up mail server details…`, click `Next`
4. Select **Server Type**: `Exchange Web Services`
  - Set **Host URL**: `https://outlook.office365.com/EWS/Exchange.asmx`
  - Click **Check for Supported Types** - this should select `OAuth2 (Office 365)`
  - **Check** `Override Office 365 OAuth2 settings`
  - Enter the **Tenant ID** of your account (copy the `tid` query parameter value from your account url in Outlook Web Access)
  - Open the [**Help…**](https://wiki.gnome.org/Apps/Evolution/EWS/OAuth2) link and follow the instructions provided there.

In case you run into any troubles due to the Evolution application ID not beeing authorized by your Office 365 administrator, use the last Evolution application ID with the
Redirect URI set to `urn:ietf:wg:oauth:2.0:oob` [as descrdibed in the GNOME Wiki](https://wiki.gnome.org/Apps/Evolution/EWS/OAuth2).

**Unified Inbox in Evolution**

To have a grouped inbox view in Evolution I am going to use the `Search Folders` feature. Go to `Edit > Preferences` and enable `Search Folders`. Then drag it the top. Then create a new Search Folder in `Edit > Search Folders > Add` with the following settings:

- Rule name: `Inbox`
- Find items which match: `any of the following conditions`
- Include threads: `None`
- `Message Location`: `is`: `Your Account/Inbox`
  - Add as many `Message Location` conditions as you have accounts and inboxes
- **Check** Automatically update on any source folder change
- Select `All active remote folders`
- Then click **Ok**

Repeat the above steps for any Unified Folder you want to have (e.g. for `Archive`).

## Microsoft Teams

Install the [Microsoft Teams application from Flathub](https://flathub.org/apps/details/com.microsoft.Teams):

```shell
flatpak install flathub com.microsoft.Teams
```

## Cryptomator

Install the [Cryptomator application from Flathub](https://flathub.org/apps/details/com.microsoft.Teams):

```shell
flatpak install flathub org.cryptomator.Cryptomator
```

## all-ways-egpu

Install this script to configures an eGPU as primary under Wayland desktops [as documented in the repo](https://github.com/ewagner12/all-ways-egpu):

```shell
cd ~; curl -qLs  https://github.com/ewagner12/all-ways-egpu/releases/latest/download/all-ways-egpu.zip  -o all-ways-egpu.zip; unzip all-ways-egpu.zip; cd all-ways-egpu-main; chmod +x install.sh; sudo ./install.sh install; cd ../; rm -rf all-ways-egpu.zip all-ways-egpu-main
```

And then run the setup:

```shell
all-ways-egpu setup

Is this the eGPU to be used as primary? [y/N]
# Choose "y" for your eGPU, "N" for all other detected devices

Identify all iGPU/dGPUs to be potentially disabled at boot:
# Don't disable any device during boot - choose "N" for all of them

Manual Setup: Enter Bus IDs and drivers in the following example format or enter 'n' to skip.
# Enter "n" to skip

Recommended if using Method 1: Attempt to re-enable the iGPU/initially disabled devices after login? [y/N]
# Enter "N" to not re-enable

Recommended if using Method 2: Attempt to set boot_vga flag at startup? [y/N]
# Enter "y" to set boot_vga flag
```

After each re-boot you will have to enable the eGPU manually. To do so, open a Terminal and execute the following:

```shell
all-ways-egpu

Enter Choice [1-9]:
4 # Set boot-vga Flag (Method 2)

Enter Choice [1-3]:
1 # Set boot-vga Flag to eGPU
```

Then restart your Display Manager by logging out and logging in again.

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