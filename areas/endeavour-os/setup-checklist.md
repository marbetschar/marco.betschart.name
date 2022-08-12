---
description: My personal checklist for setting up a fresh Endeavour OS installation.
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

