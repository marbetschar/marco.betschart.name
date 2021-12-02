---
description: How to install Oracle SQL Developer in your Linux Desktop Environment.
tags:
  - how-to
  - elementary
  - sql-developer
  - oracle
  - linux-desktop
---

# Install Oracle SQL Developer

> **Verified For:** elementary OS 6.0 Odin

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Prerequisites

To be able to execute Oracle SQL Developer we need an installed JDK. The following command will install the Java OpenJDK:

```bash
sudo apt install openjdk-17-jdk
```

## Download

Download Oracle SQL Developer for "Other Platforms" from Oracle:

* [https://www.oracle.com/tools/downloads/sqldev-downloads.html](https://www.oracle.com/tools/downloads/sqldev-downloads.html)

## Extract

After the download is completed, extract the `~/Downloads/sqldeveloper-*.zip` to `~/Applications/sqldeveloper`.

## Integrate

As last step, we are create a desktop integration file in `~/.local/share/applications/sqldeveloper.desktop`:

{% hint style="warning" %}
Replace _USER_ with your actual username.
{% endhint %}

```text
[Desktop Entry]
Name=Oracle SQL Developer
Comment=SQL Developer from Oracle
GenericName=SQL Tool
Exec=/home/USER/Applications/sqldeveloper/sqldeveloper/bin/sqldeveloper $*
Icon=/home/USER/Applications/sqldeveloper/icon.png
Type=Application
StartupNotify=true
Categories=Utility;Oracle;Development;SQL;
```

That's it: You've completed the installation of Oracle SQL Developer for your Linux Desktop Environment.

