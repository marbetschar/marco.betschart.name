---
description: How to setup a HP laser printer on elementary OS.
tags:
  - how-to
  - elementary
  - printer
  - linux-desktop
---

# Setup HP Color Laser Jet Pro MFP M281 fdw

> ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20Jólnir-007aff)
> ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Printing

In order to be able to print with a HP Color Laser Jet Pro MFP M281 fdw on elementary OS 6.1, you don't have to do anything. It works right out of the box.

## Scanning

Even though the printer itself works out of the box, you need to install a proprietary plugin from HP to be able to scan anything. Because HPLIP added
official support for elementary OS 6.1 in a newer HPLIP version, the easiest way to do so is to update the installed HPLIP version.

To do so, go to the [HPLIP download page](https://developers.hp.com/hp-linux-imaging-and-printing/gethplip) and download the latest version for
elementary OS (v3.22.2 at the time of this writing).

For installation, execute the following commands in your Terminal:

```bash
chmod 755 ~/Downloads/hplip-*.run
~/Downloads/hplip-*.run

...

HP Linux Imaging and Printing System (ver. 3.22.2)

...

INSTALLATION MODE
-----------------
Automatic mode will install the full HPLIP solution with the most common options.
Custom mode allows you to choose installation options to fit specific requirements.

Please choose the installation mode (a=automatic*, c=custom, q=quit) : a

...

DISTRO/OS CONFIRMATION
----------------------
Distro appears to be Elementary OS 6.1.

Is "Elementary OS 6.1" your correct distro/OS and version (y=yes*, n=no, q=quit) ? y

...

SECURITY PACKAGES
-----------------
AppArmor is installed. 
AppArmor protects the application from external intrusion attempts making the application secure

Would you like to have this installer install the hplip specific policy/profile (y=yes*, n=no, q=quit) y

...

HPLIP-3.20.3 exists, this may conflict with the new one being installed.
Do you want to ('i'= Remove and Install*, 'q'= Quit)?    : i
Starting uninstallation...

...

Done.
```

Now we are finally ready to download the proprietary plugin with the following command:

```bash
$ hp-plugin -i

HP Linux Imaging and Printing System (ver. 3.22.2)
Plugin Download and Install Utility ver. 2.1

...

-----------------------------------------
| PLUG-IN INSTALLATION FOR HPLIP 3.22.2 |
-----------------------------------------

The driver plugin for HPLIP 3.22.2 appears to already be installed.
Do you wish to download and re-install the plug-in? (y=yes*, n=no, q=quit) ? yerror:  No system tray detected on this system.  Unable to start, exiting. 

  Option      Description                                       
  ----------  --------------------------------------------------
  d           Download plug-in from HP (recommended)            
  p           Specify a path to the plug-in (advanced)          
  q           Quit hp-plugin (skip installation)                

Enter option (d=download*, p=specify path, q=quit) ? d

...

Do you accept the license terms for the plug-in (y=yes*, n=no, q=quit) ? y

Done.
```

## Further Reading

* [bugs.launchpad.net/hplip/+bug/1822762](https://bugs.launchpad.net/hplip/+bug/1822762#yui_3_10_3_1_1626764399201_586)
* [HPLIP Release Notes](https://developers.hp.com/hp-linux-imaging-and-printing/release_notes)
