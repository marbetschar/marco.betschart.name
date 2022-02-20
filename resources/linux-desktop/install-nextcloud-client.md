---
description: How to install Nextcloud Client on elementary OS.
tags:
  - how-to
  - elementary
  - nextcloud
  - linux-desktop
---

# Install Nextcloud Client

> ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20Jólnir-007aff)
> ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

- [Install Flatpak](#install-flatpak)
- [Install from PPA](#install-from-ppa)
- [Start and Configure](#start-and-configure)

![elementary Files Nextcloud integration](../../.gitbook/assets/elementary-files-cloud-provider-nextcloud.png)

## Install Flatpak

* [ ] Click `Install` on [Nextcloud Desktop's FlatHub.org page](https://flathub.org/apps/details/com.nextcloud.desktopclient.nextcloud)
* [ ] Choose `Open with Sideload`
* [ ] Select `I understand` and click `Install Anyway`
* [ ] Select `Move *.flatpakref to Trash` and click `Open App`

## Install from PPA

{% hint style="warning" %}
**DEPRECATED:** Please prefer installing from Flathub, because PPA's are not officially supported on elementary OS.
{% endhint %}

### Add Nextcloud client PPA

You need to add the Nextcloud client PPA to enable your elementary OS to actually find the needed packages. For this, open a Terminal and insert the following commands:

```text
sudo apt install software-properties-common    # installs the "add-apt-repository" command
sudo add-apt-repository ppa:nextcloud-devs/client
```

For more details see [the PPA's homepage](https://launchpad.net/~nextcloud-devs/+archive/ubuntu/client).

### Install Nextcloud client

_Don't worry, you only need to install Nextcloud client via Terminal - future updates will be handled graphically by the elementary OS AppCenter._

We are now ready to install the client. To do so, enter the following commands in your Terminal:

```text
sudo apt install nextcloud-client
```

## Start and Configure

And that's it. You successfully installed Nextcloud client on elementary OS. Start it up and configure it. Once you fully configured it, you'll fall in love with its integration into elementary's File Manager.
