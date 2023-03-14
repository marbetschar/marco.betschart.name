---
description: How to setup different printers and scanners on elementary OS.
tags:
  - how-to
  - printer
  - scanner
  - linux-desktop
---

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Brother MFC-L2710DW

> ![Arch Linux](https://img.shields.io/badge/arch%C2%A0linux-007aff)

Install the [`brother-mfc-l2710dw` package from AUR](https://aur.archlinux.org/packages/brother-mfc-l2710dw):

```shell
yay brother-mfc-l2710dw
```

Then start the printing service (cups) and make sure it autostarts on boot:

```shell
# Autostart at Boot:
sudo systemctl enable cups

# Start Now:
sudo systemctl start cups

# IMPORTANT: If you get an error when starting cups, try to run cups manually as root.
# It will print the reason why it failed. For example:
# $ sudo /usr/bin/cupsd -l
# /usr/bin/cupsd: error while loading shared libraries: libpaper.so.2: cannot open shared object file: No such file or directory
```

You are now ready to add the printer by:

- Navigating to [http://localhost:631](http://localhost:631), `Administration > Add Printer`
- Login with our username and password
- Select `AppSocket/HP JetDirect`
- Enter `socket://123.456.78.90:9100`, click `Continue`
- Enter the printer's name `Brother-MFC-L2710DW`
- Select Make `Brother` and Model `Brother MFCL2710DW` and click `Add Printer`


Since the printer is working now, lets enable its scanner. To do so, install [brscan4 from AUR](https://aur.archlinux.org/packages/brscan4):

```shell
yay brscan4
```

Then configure it with:

```shell
sudo brsaneconfig4 -a name=MFCL2710DW model=MFCL2710DW ip=123.456.78.90
```

Test whether it works:

```shell
scanimage -L
```

And last but not least install `simple-scan` to use a simple UI for scanning:

```shell
sudo pacman -S simple-scan
```

> ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20Jólnir-007aff)

Download the latest "Driver Install Tool" for Linux from the [Brother MFC-L2710DW download page](https://support.brother.com/g/b/downloadtop.aspx?c=us_ot&lang=en&prod=mfcl2710dw_us_eu_as)  (`linux-brprinter-installer-2.2.3-1.gz` at the time of this writing).

Then install the drivers as documented on the download page (open the Terminal and execute the following commands):

```bash
# Change to the download directory:
cd ~/Downloads

# Extract the downloaded file
gunzip linux-brprinter-installer-*.gz

# Make the extracted shell script executable
chmod +x linux-brprinter-installer-*

# Run the install tool with the printer type with root permissions:
sudo ./linux-brprinter-installer-* MFC-L2710DW
You are going to install following packages.
   mfcl2710dwpdrv-4.0.0-1.i386.deb
   brscan4-0.4.11-1.amd64.deb
   brscan-skey-0.3.1-2.amd64.deb
OK? [y/N] -> y
...
Do you agree? [Y/n] -> Y
...
# For USB Users: Choose N(No)
# For Network Users: Choose Y(Yes) and DeviceURI number.
Will you specify the Device URI? [Y/n] -> Y
...
0: cups-brf:/
1: lpd
2: http
3: socket
4: hp
5: beh
6: ipps
7: https
8: ipp
9: dnssd://Brother%20MFC-L2710DW%20series._ipp._tcp.local/?uuid=e3248000-80ce-11db-8000-3c2af4943c7a
10: lpd://BRW802BF9F1CFD8/BINARY_P1
11: ipp://Brother%20MFC-L2710DW%20series._ipp._tcp.local/
12 (I): Specify IP address.
13 (A): Auto. (dnssd://Brother%20MFC-L2710DW%20series._ipp._tcp.local/?uuid=e3248000-80ce-11db-8000-3c2af4943c7a)

select the number of destination Device URI. -> 13
...
Test Print? [y/N] -> y
...
You are going to install following packages.
   brscan4-0.4.11-1.amd64.deb
...
Do you agree? [Y/n] -> Y
...
You are going to install following packages.
   brscan-skey-0.3.1-2.amd64.deb
...
Do you agree? [Y/n] -> Y
...
Setting up brscan-skey (0.3.1-2) ...
 enter IP address -> 192.168.1.234    # Enter the printer's IP address
```

## HP Color Laser Jet Pro MFP M281 fdw

> ![elementary OS: 6.1 Jólnir](https://img.shields.io/badge/elementary%C2%A0OS-6.1%20Jólnir-007aff)
> ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

### Printing

In order to be able to print with a HP Color Laser Jet Pro MFP M281 fdw on elementary OS 6.1, you don't have to do anything. It works right out of the box.

### Scanning

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

### Further Reading

* [bugs.launchpad.net/hplip/+bug/1822762](https://bugs.launchpad.net/hplip/+bug/1822762#yui_3_10_3_1_1626764399201_586)
* [HPLIP Release Notes](https://developers.hp.com/hp-linux-imaging-and-printing/release_notes)
