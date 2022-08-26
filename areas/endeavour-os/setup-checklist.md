---
description: My personal checklist for setting up a fresh Endeavour OS installation.
---

# Setup Checklist

## Multiboot with Full Disk Encryption

If you are running [multiple operating systems with full disk encryption](../elementary-os/dual-boot-elementary-windows-with-full-disk-encryption.md),
the following snippet will come in handy to allow all of the to boot after EndeavourOS was installed on your machine:

```diff
# (Required) After booting into Endeavour OS:

# Make sure os-prober runs first to prioritize other
# operating systems over EndeavourOS:
sudo mv /etc/grub.d/30_os-prober /etc/grub.d/05_os-prober

# Windows is always first (= 0) detected by os-prober,
# so make elementary OS the default (= 1):
sudo vi /etc/default/grub
#GRUB_DEFAULT=0
GRUB_DEFAULT=1

# Decrypt elementary partition to enable os-prober
# its detection:
yay update-grub
sudo cryptsetup luksOpen /dev/nvme0n1p6 elementary
sudo update-grub

# (Optional) After booting into elementary OS:
# Disable update-grub after kernel install/remove
sudo chmod a-x /etc/kernel/postinst.d/zz-update-grub
sudo chmod a-x /etc/kernel/postrm.d/zz-update-grub
```

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
* [ ] [GitLab.com](https://gitlab.com/-/profile/keys)
* [ ] [GNOME GitLab](https://gitlab.gnome.org/-/profile/keys)

## VSCodium

Install VSCodium from AUR by executing the following command in the Terminal:

```shell
yay vscodium-bin
```

## AppImageLauncher

Install AppImageLauncher from AUR by executing the following command in the Terminal:

```shell
yay appimagelauncher-git
```

## Paymo

* [ ] [Download the Paymo Desktop App from the Website](https://www.paymoapp.com/downloads-and-integrations/)
* [ ] Open the downloaded AppImage in Files \(double click\)
  * [ ] If prompted, confirm `~/Applications` as integration target destination directory
* [ ] Click `Integrate and run`
* [ ] Login to Paymo Account

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