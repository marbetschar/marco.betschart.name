---
description: My personal checklist for setting up a fresh Fedora Workstation installation.
---

# Setup Checklist

Tested on Fedora Workstation 44, RTX 5060 Ti eGPU, ThinkPad X1 Yoga

## Base System Fedora Everything 44

1. [Download Fedora Everything 44](https://fedoraproject.org/misc/#minimal)
2. **Install**:
   - Select **"Fedora Custom Operation System"**
     - AND **Common NetworkManager Submodules**
     - AND **Standard** (common set of utilities)
   - **Partitioning**: Use automatic (Btrfs)
   - **User**: Create your account with `sudo` access

## Fix Wifi

```bash
nmcli device status
```

In case this does not list the WiFi device, connect your Hotspot via USB Tethering and run the following commands:

```bash
wget https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/plain/intel/iwlwifi/iwlwifi-so-a0-gf-a0-89.ucode
wget https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/plain/intel/iwlwifi/iwlwifi-so-a0-gf-a0.pnvm

sudo mv iwlwifi-so-* /lib/firmware/

sudo chown root:root /lib/firmware/iwlwifi-so-*
sudo chmod 644 /lib/firmware/iwlwifi-so-*

sudo modprobe -r iwlwifi
sudo modprobe iwlwifi
````

Then, check again and connect to your WLAN:

```bash
nmcli device status
nmcli device wifi connect <SSID> --ask
```

## Install Desktop

After first boot, run the following commands on the command line:

```bash
sudo dnf install niri niri-settings
sudo dnf install --nogpgcheck --repofrompath 'terra,https://repos.fyralabs.com/terra$releasever' terra-release
sudo dnf install noctalia-shell
sudo dnf install noctalia-greeter
# Use Kitty as Terminal Emulator:
sudo dnf install kitty
sudo dnf remove alacritty
```

Start Noctalia from Niri:

```
# ~/.config/niri/config.kdl:
spawn-at-startup "qs" "-c" "noctalia-shell"
...
# Mod+T hotkey-overlay-title="Open a Terminal: alacritty" { spawn "alacritty"; }
Mod+T hotkey-overlay-title="Open a Terminal" { spawn "kitty"; }
```

Then make sure to configure greetd:

```
# /etc/greetd/config.toml:
[terminal]
vt = 1

[default_session]
command = "env XKB_DEFAULT_LAYOUT=ch /usr/bin/noctalia-greeter-session"
user = "greetd"
```

And finally boot into your lightweight Niri + Noctalia desktop:

```bash
sudo systemctl set-default graphical.target
sudo systemctl enable greetd --now
```

## Fix Sound

In case you don't have any sound, fix it with:

```bash
sudo dnf install alsa-sof-firmware

echo "options snd-intel-dspcfg dsp_driver=3" | sudo tee /etc/modprobe.d/use-sof.conf
sudo dracut --regenerate-all --force
sudo grubby --update-kernel=ALL --args="snd-intel-dspcfg.dsp_driver=3"
sudo reboot
```

## Configure Fingerprint Reader

```bash
sudo dnf install fprintd
sudo fprintd-enroll $USER
sudo authselect enable-feature with-fingerprint
sudo authselect select apply-changes
sudo systemctl enable --now fprintd
```

## Make sure GTK apps prefer dark theme

```bash
gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark'
```

## AppImageLauncher

1. Download RPM from [GitHub Release page](https://github.com/TheAssassin/AppImageLauncher/releases)
2. Install the RPM with `sudo dnf install $HOME/Downloads/appimagelauncher_*.rpm`

## Paymo

[Downoad Paymo Track from their Website](https://www.paymoapp.com/downloads/) and integrate the AppImage using the installed AppImageLauncher.

## Online Accounts

```bash
sudo dnf install evolution evolution-ews
```

**Study & Work**

1. Start Evolution
2. Start the New Mail Account Wizard: Click `File > New > Mail Account`
3. Enter your **Email Address** and **uncheck** `Look up mail server details…`, click `Next`
4. Select **Server Type**: `Exchange Web Services`

* Set **Host URL**: `https://outlook.office365.com/EWS/Exchange.asmx`
* Click **Check for Supported Types** - this should select `OAuth2 (Office 365)`
* **Check** `Override Office 365 OAuth2 settings`
* Keep default values in OAuth2 setting fields

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

Repeat the above steps for any Unified Folder you want to have (e.g. for `Archive`)

**Private**

* [ ] `Nextcloud` for Calendar and Contacts (needs application specific password)
* [ ] `IMAP and SMTP` for Mail

|                        |     Server     | Port | Encryption |
| ---------------------- | :------------: | :--: | :--------: |
| _Incoming Mail (IMAP)_ | imappro.zoho.eu |  993 |     STARTTLS    |
| _Outgoing Mail (SMTP)_ | smtp.zoho.eu |  587 |  STARTTLS  |

[_zoho.com/mail/help/imap-access_](https://www.zoho.com/mail/help/imap-access.html)

## eGPU: RTX 5060 Ti

1. Plugin eGPU
2. Authorize Thunderbolt:
   ```bash
   sudo dnf install bolt
   boltctl list
   # if the device is not authorized:
   boltctl authorize DEVICE_UUID
   boltctl enroll DEVICE_UUID # store permanently
   ```
3. Install `nvidia-open` according to [NVIDIA's instructions](https://docs.nvidia.com/datacenter/tesla/driver-installation-guide/fedora.html) 
4. Reboot
5. `nvidia-smi` should now show the GPU

**Enable eGPU Hotplug**

Edit `/etc/default/grub` and add these parameters to `GRUB_CMDLINE_LINUX`:

```text
pcie_ports=native hpbussize=0x33,realloc,hpmmiosize=128M,hpmmioprefsize=512M
```

Then update GRUB:

```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```