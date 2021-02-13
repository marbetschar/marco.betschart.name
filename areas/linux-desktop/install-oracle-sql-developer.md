---
description: How to install Oracle SQL Developer in your Linux Desktop Environment.
tags: 'how-to, elementary, sql-developer, oracle, linux-desktop'
---

# Install Oracle SQL Developer

![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff) ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me on GitHub**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Java Open JDK

Execute the following command to install the Java OpenJDK:

```bash
sudo apt install openjdk-14-jdk
```

## Oracle SQL Developer

Download Oracle SQL Developer for "Other Platforms" from the [Oracle Website](https://www.oracle.com/tools/downloads/sqldev-downloads.html) to `~/Downloads`. After the download is completed, execute the following commands to install Oracle SQL Developer to `/opt`:

```bash
cd /opt
sudo unzip ~/Downloads/sqldeveloper-*.zip
sudo ln -s /opt/sqldeveloper/sqldeveloper.sh /usr/local/bin/sqldeveloper
```

Then we need to update the `sqldeveloper.sh` file, to allow execution from any directory:

```diff
#!/bin/bash
-cd "`dirname $0`"/sqldeveloper/bin && bash sqldeveloper $*
+/opt/sqldeveloper/sqldeveloper/bin/sqldeveloper $*
```

As last step, we are create a desktop integration file in `/usr/share/applications/sqldeveloper.desktop`:

```text
[Desktop Entry]
Name=Oracle SQL Developer
Comment=SQL Developer from Oracle
GenericName=SQL Tool
Exec=/usr/local/bin/sqldeveloper
Icon=/opt/sqldeveloper/icon.png
Type=Application
StartupNotify=true
Categories=Utility;Oracle;Development;SQL;
```

That's it: You've completed the installation of Oracle SQL Developer for your Linux Desktop Environment.

