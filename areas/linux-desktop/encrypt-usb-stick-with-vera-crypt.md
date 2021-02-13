---
description: How to encrypt an USB stick using Vera Crypt.
tags: 'how-to, open-source, encryption, elementary'
---

# Encrypt USB Stick with Vera Crypt

![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff) ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me on GitHub**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

* [Installation](encrypt-usb-stick-with-vera-crypt.md#installation)
* [Traveler Disk Setup](encrypt-usb-stick-with-vera-crypt.md#traveler-disk-setup)
* [Troubleshooting](encrypt-usb-stick-with-vera-crypt.md#troubleshooting)
* [Further Reading](encrypt-usb-stick-with-vera-crypt.md#further-reading)

## Installation

VeraCrypt is not available on the default Ubuntu repositories. Therefore, to install it using the package manger, you have to add the PPA repositories.

Add PPA repos using the command below. Note that this repository is not related to VeraCrypt even though Unit 193 is Xubuntu developer and he is a great contributor to the open source community;

```text
sudo add-apt-repository ppa:unit193/encryption
sudo apt-get update
sudo apt install veracrypt
```

## Traveler Disk Setup

**PLEASE NOTE:** Since we are not using Windows, there is no `Tools > Traveler Disk Setup` option. This is expected. Nevertheless, we can create the Traveler Disk manually:

> ... For linux and MAC this option is not available, but the apps are already portable. I just had to copy the executables from `/usr/bin` in Linux and `Applications` in OSX. I've tested them on clean system where TrueCrypt wasn't installed. [**- Ask Ubuntu: Create veracrypt traveler disk in Ubuntu**](https://askubuntu.com/questions/847127/create-veracrypt-traveler-disk-in-ubuntu)

### Partition the USB Stick

The first step is to create two Partitions on your USB Stick:

* a small one called `Travel-Disk` using the `NTFS` file system and is `512 MB` in size
  * this partition won't be encrypted; It will provide the VeraCrypt binaries
* a big one claiming all of the remaining space of your USB Stick
  * we are going to encrypt this partition in a minute

### Copy VeraCrypt binaries

Next we'll transfer the VeraCrypt binaries to the `Travel-Disk` Partition. Below we are assuming it is mounted under `/media/$USER/Travel-Disk`.

#### Linux

```bash
# Create a Linux directory:
mkdir /media/$USER/Travel-Disk/Linux

# Copy the veracrypt binary:
cp /usr/bin/veracrypt /media/$USER/Travel-Disk/Linux/

# Create a brief README:
cat > /media/$USER/Travel-Disk/Linux/README.md << 'EOF'
# VeraCrypt for Linux

Execute the veracrypt binary from your Terminal:

sh -c /media/$USER/Travel-Disk/Linux/veracrypt
EOF
```

#### macOS

Unfortunately for macOS there is no standalone version available, because macFUSE 3.10 or newer must be installed too. So the best we can do is to [download the latest stable VeraCrypt DMG file](https://www.veracrypt.fr/en/Downloads.html) along with the [latest stable macFuse](https://github.com/osxfuse/osxfuse/releases) and copy both files to `Travel-Disk` together with a brief README file:

```bash
# Create a macOS directory:
mkdir /media/$USER/Travel-Disk/macOS

# Copy the VeraCrypt DMG file:
cp ~/Downloads/VeraCrypt*.dmg /media/$USER/Travel-Disk/macOS/

# Copy the macFuse DMG file:
cp ~/Downloads/macfuse*.dmg /media/$USER/Travel-Disk/macOS/

# Create a brief README:
cat > /media/$USER/Travel-Disk/macOS/README.md << 'EOF'
# VeraCrypt for macOS

No standalone version available.
macFUSE 3.10 or newer must be installed too.
EOF
```

#### Windows

There is a portable version available for Windows, so we download the [latest stable version](https://www.veracrypt.fr/en/Downloads.html) and copy it to `Travel-Disk/Windows`:

```bash
# Create a Windows directory:
mkdir /media/$USER/Travel-Disk/Windows

# Copy the VeraCrypt Portable exe file:
cp ~/Downloads/VeraCrypt*.exe /media/$USER/Travel-Disk/Windows/

# Create a brief README:
cat > /media/$USER/Travel-Disk/Windows/README.md << 'EOF'
# VeraCrypt for Windows

IMPORTANT: DON'T EXTRACT THE APP TO THE USB STICK!

Because the VeraCrypt driver is not unloaded
after exiting VeraCrypt, you won't be able to
unmount the stick without a system reboot.

https://www.veracrypt.fr/en/Portable%20Mode.html
EOF
```

### Create encrypted partition

Now everything is ready to create the encrypted partition:

1. Start VeraCrypt
2. Go to `Tools > Volume Creation Wizard`
3. Select `Create a Volume within a partition/drive`
4. Select `Standard VeraCrypt volume`
5. In **Volume Location**, click `Select Device...`
   * then select the previously created, big partition \(probably /dev/sda2\)
6. Enter the local machine's Administrator password when prompted
7. In **Encryption Options** make sure to select [something different than the defaults](https://blog.elcomsoft.com/2020/03/breaking-veracrypt-containers/)
8. Then set your **Volume Password**
9. `Enable` Large File support
10. Choose `NTFS` as the **Filesystem Type**
11. `Enable` **Cross-Platform Support**
12. Format the Volume
13. Click `Exit` - and you're done

## Further Reading

* [VeraCrypt Documentation](https://www.veracrypt.fr/en/Documentation.html)
* [Create veracrypt traveler disk in Ubuntu](https://askubuntu.com/questions/847127/create-veracrypt-traveler-disk-in-ubuntu)
* [How to work with DMG files on Linux](https://eastmanreference.com/how-to-work-with-dmg-files-on-linux)
* [Breaking VeraCrypt containers](https://blog.elcomsoft.com/2020/03/breaking-veracrypt-containers/)

