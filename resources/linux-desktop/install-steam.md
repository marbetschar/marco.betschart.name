---
description: How to install Steam in your Linux Desktop Environment.
tags:
  - how-to
  - elementary
  - steam
  - linux-desktop
---

# Install Steam

![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff) ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

Because Steam is 32-bit only, you first need to enable i386 multiarch and be sure you are up-to-date:

```bash
sudo dpkg --add-architecture i386
sudo add-apt-repository multiverse
sudo apt update
```

Then install Steam:

```bash
sudo apt install steam
```

## Source

* [lubuntu installing steam "steam has no installation candidate"](https://askubuntu.com/questions/958957/lubuntu-installing-steam-steam-has-no-installation-candidate#958965)

