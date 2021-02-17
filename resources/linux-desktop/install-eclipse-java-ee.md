---
description: >-
  How to install Eclipse Java Enterprise Edition on your Linux Desktop
  Environment.
tags:
  - how-to
  - elementary
  - nextcloud
  - linux-desktop
---

# Install Eclipse Java EE

![elementary OS: 6 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6%20Odin-007aff) ![Status: Verified](https://img.shields.io/badge/status-verified-green.svg)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me on GitHub**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Download

Download the Eclipse IDE for Enterprise Java Developers from the following URL \(Linux x86\_64\):

* [https://www.eclipse.org/downloads/packages/](https://www.eclipse.org/downloads/packages/)

## Extract

Extract the downloaded \*`.tar.gz` file to `~/Applications/eclipse`

## Integrate

As last step, create a Desktop Shortcut for your Launcher. To do so, create a new `~/.local/share/applications/eclipse.desktop` file:

{% hint style="warning" %}
Replace _USER_ with your actual username.
{% endhint %}

```text
[Desktop Entry]
Name=Eclipse Java EE
Comment=Eclipse IDE for Enterprise Java Developers
GenericName=Java IDE
Exec=/home/USER/Applications/eclipse/eclipse
Icon=/home/USER/Applications/eclipse/icon.xpm
Type=Application
StartupNotify=true
Categories=Utility;Java;Development;IDE;
```