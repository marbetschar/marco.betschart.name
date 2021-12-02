---
description: How to setup a HP laser printer on elementary OS.
tags:
  - how-to
  - elementary
  - printer
  - linux-desktop
---

# Setup HP Color Laser Jet Pro MFP M281 fdw

> ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)
> ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Printing

In order to be able to print with a HP Color Laser Jet Pro MFP M281 fdw on elementary OS 6, you don't have to do anything. It works right out of the box.

## Scanning

Even though the printer itself works out of the box, you need to install a proprietary plugin from HP to be able to scan anything. To do so, execute the following command in your Terminal:

```bash
$ sudo hp-plugin -i

HP Linux Imaging and Printing System (ver. 3.20.3)
Plugin Download and Install Utility ver. 2.1

...

-----------------------------------------
| PLUG-IN INSTALLATION FOR HPLIP 3.20.3 |
-----------------------------------------

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

