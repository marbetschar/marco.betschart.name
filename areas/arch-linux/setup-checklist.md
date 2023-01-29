---
description: My personal checklist for setting up a fresh Arch Linux installation.
---

# Setup Checklist

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

## Paymo Widget

Install the Paymo Widget from AUR by executing the following command in the Terminal:

```shell
yay paymo-widget
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