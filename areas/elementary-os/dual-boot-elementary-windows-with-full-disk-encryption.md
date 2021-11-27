---
description: >-
  Howto dual boot Windows alongside elementary OS with full disk encryption enabled for both operating systems.
tags:
  - setup
  - elementary
  - windows
  - security
  - encryption
  - luks
  - bitlocker
---

# Dual Boot elementary OS and Windows with Full Disk Encryption

{% hint style="warning" %}
**BE AWARE:** For this approach to work, we need an *un-*encrypted boot partition. This still allows for
some attacks to work such as the [Evil Maid Attack](https://www.schneier.com/blog/archives/2009/10/evil_maid_attac.html).
But the primarily goal here is to protect your data against physical theft - not a coup executed by a 3-letter-organisation.
{% endhint %}

## 1. Prerequisites

We will need to boot into Windows and elementary OS multiple times during this setup. Therefore it is recommended to create a dedicated installation media for each operating system.

### 1.1 Create a bootable elementary OS USB stick

1. Download the elementary OS *.iso from https://elementary.io
2. Follow the instructions in the elementary OS [Installation Guide](https://elementary.io/docs/installation#creating-an-installation-medium) to create the Install Drive

### 1.2 Create a bootable Windows 10 USB stick

The following applies if you are already on elementary OS. If not, please search for a corresponding guide for your current operating system:

1. Download the Windows 10 *.iso from https://www.microsoft.com/software-download/windows10
2. Download the latest WoeUSB release (`woeusb-x.y.z.bash`) from https://github.com/WoeUSB/WoeUSB/releases
3. Install WoeUSB dependencies for Ubuntu, [as described in the WoeUSB wiki](https://github.com/WoeUSB/WoeUSB/wiki/Dependencies#ubuntu)
4. Make sure `woeusb-*.bash` and `Win10_*.iso` are stored in `~/Downloads`
5. Make WoeUSB executable: `chmod +x ~/Downloads/woeusb-*.bash`
6. Plugin the USB stick you want to overwrite
7. Figure out the device name of the USB stick by executing `sudo fdisk -l` from Terminal (in my case its `/dev/sda`)
8. Create the Windows 10 USB stick: `~/Downloads/woeusb-*.bash --device ~/Downloads/Win10_*.iso /dev/sdX`
9. Done.

### 1.3 Completely Wipe Hard Drive (Recommended, Optional)

While this step is optional, it is highly recommended to wipe the entire hard drive before starting this setup. This ensures your complete hard drive is filled
with random data, which makes it much harder to decrypt your data after your completed this setup. It also makes sure you don't have any remainings of a (potential)
previous install on your hard disk.

To do so, we boot elementary OS in Demo Mode:

1. Boot from elementary OS USB stick
2. After the installer starts:
   - Select your language
   - Select your keyboard layout
3. On the "Try or Install" step, choose "Try Demo Mode" and confirm

Once elementary OS is booted, start "GParted" from the Applications Menu.

In GParted:

4. Delete all available partitions
5. Create a new partition which occupies the entire hard disk (just use the default file system)
6 . Click "Apply All Operations". You should end up with one partition

In my case the partition device is named `/dev/nvme0n1p1`.

At this point we need to fall back to the Terminal, because GParted is [not able to create encrypted LUKS containers yet](https://gparted.org/features.php).
Open the Terminal and run the following commands:

```bash
# Create a LUKS container ("luksFormat" is case sensitive):
sudo cryptsetup luksFormat /dev/nvme0n1pX

# Open the previously created LUKS container with name 'cryptdrive' ("luksOpen" is case sensitive):
sudo cryptsetup luksOpen /dev/nvme0n1pX cryptdrive

# Wipe entire cryptdrive by fill it completely with random data (this took about 1h on my 1TB drive):
sudo dd if=/dev/zero of=/dev/mapper/cryptdrive bs=16M

# Close the LUKS container ("luksClose is case sensitive):
sudo cryptsetup luksClose cryptdrive
```

## 2. Partitioning

### 2.1 Boot elementary OS in Demo Mode

Since we are going to create encrypted LUKS containers, we need to boot elementary OS in Demo Mode to do the partitioning:

1. Boot from elementary OS USB stick
2. After the installer starts:
   - Select your language
   - Select your keyboard layout
3. On the "Try or Install" step, choose "Try Demo Mode" and confirm

### 2.2 Create Partitions in GParted

**IMPORTANT:** There's currently no easy way to make grub work with an encrypted partition.
**Therefore make sure `/boot` and `/boot/EFI` are their own partitions and are _not_ encrypted**.

Once elementary OS is booted, start "GParted" from the Applications Menu. Then in GParted:

1. Delete all already existing partitions and click `Apply All Operations`
2. Create a new GPT partition table (required for EFI):
  - `Device > Create Partition Table`
  - Select new partition table type: `gpt`
  - Click `Apply`
3. Create the following partitions:
  - 550 MiB FAT32 (for `/boot/EFI`)
  - 500 MiB EXT4 (for `/boot`)
  - X GiB NTFS (for Windows)
  - **Leave any remaining space unallocated**
    - Windows will add another 16 MiB partition upon its installation, therefore we create the partition for elementary OS later on
  - Click `Apply All Operations`
4. Mark FAT32 partition as EFI:
  - Right click on the FAT32 partition
  - In the context menu, click `Manage Flags`
  - In the new window, enable `esp` (this also enables `boot`)
  - Click `Close`

Now we are ready to install Windows!

## 3. Install Windows

**PLEASE NOTE:** Windows did not recognize my hard disk during install on a Dell XPS 9310. The solution was to change the BIOS setting `Storage Type` from `RAID` to `AHCI/NVMe` (see [this Dell community question](https://www.dell.com/community/XPS/Pros-Cons-AHCI-vs-Raid-On-XPS13-9300-NVMe/td-p/7636984) for more information about this setting).

1. Boot from the Windows USB stick
2. Install Windows to the partition you created in step 2.2.3
3. Complete the initial setup of Windows 10

Next, we are going to enable Windows Device Encryption (BitLocker):

4. Once Windows is started, open `Manage BitLocker` from the start menu
5. Click `Turn BitLocker on` to enable encryption for your Operating system drive
6. Perform the following steps to enable encryption in the BitLocker assistant:
  - Preparing your drive for BitLocker: Click `Next`
  - BitLocker Drive Encryption Setup: Click `Next`
  - How do you want to back up your recovery key?
    - Click `Print the recovery key`
    - Save the recovery key as PDF to your desktop
    - Click `Next`
  - Activate BitLocker: Click `Activate BitLocker`

**IMPORTANT:** Backup the recovery key PDF somewhere save **outside** your encrypted Windows partition! Because due to BitLocker using TPM to unlock your drive,
certain things such as a BIOS upgrade, can cause the TPM to not release the unlock-key and force you to provide the recovery key (see [How does BitLocker work without asking for a password?](https://www.quora.com/How-does-BitLocker-work-without-asking-for-a-password)).

At this point, you could install additional drivers etc. But I recommend to setup elementary OS first, because if something goes wrong you'll need to start all over again.

## 4. Install elementary OS

### 4.1 Boot elementary OS in Demo Mode

Since we are going to create encrypted LUKS containers, we need to boot elementary OS in Demo Mode:

1. Boot from elementary OS USB stick
2. After the installer starts:
   - Select your language
   - Select your keyboard layout
3. On the "Try or Install" step, choose "Try Demo Mode" and confirm

### 4.2 Create encrypted LUKS container

Next, we are going to create the encrypted LUKS partition where we are going to install elementary OS into in GParted:

1. Start "GParted" from the Applications Menu in elementary OS
2. Create a single partition with all of the remaining unallocated space - this will become the encrypted LUKS container containing all data of elementary OS
  - the file system doesn't matter yet, just use the default one
3. Click "Apply All Operations" and you'll end up with a new partition

In my case the partition device is named `/dev/nvme0n1p6`.

4. At this point we need to fall back to the Terminal, because GParted is [not able to create encrypted LUKS containers yet](https://gparted.org/features.php). Open the Terminal and run the following commands:

```bash
# LUKS: Create a container ("luksFormat" is case sensitive):
sudo cryptsetup luksFormat /dev/nvme0n1pX

# LUKS: Open the previously created container with name 'elementary' ("luksOpen" is case sensitive):
sudo cryptsetup luksOpen /dev/nvme0n1pX elementary

# Wipe entire container 'elementary' by fill it completely with random data (this took about 20mins on my 600 GiB drive):
sudo dd if=/dev/zero of=/dev/mapper/elementary bs=16M

# LVM: Create a Physical Volume
sudo pvcreate /dev/mapper/elementary

# LVM: Create a Volume Group
sudo vgcreate elementary /dev/mapper/elementary

# LVM: Create a Logical Volume which occupies all the available space (of course you can
# add multiple logical volumes with different sizes like swap, home, root etc. if you want)
sudo lvcreate --name root --extends 100%FREE elementary
```

### 4.3 Install

1. Start "Install elementary OS" from the Applications Menu in elementary OS Demo Mode
2. Confirm Logout
3. Select your language
4. Select your keyoard layout
5. Select `Custom Install (Advanced)`

To make things bootable, we need to assign the `/boot/uefi` and `/boot` mount points. Those will be stored in the first two partitions we created in 2.1.3 on the **non-encrypted, physical hard drive**:

6. Click on the 550 MiB fat32 partition on the non-encrypted, physical hard drive:
  - Enable `Use Partition`
  - **!! DON'T `Format` !!**
  - Use as: `Boot (/boot/efi)`
  - Filesystem: `fat32`
7. Click on the 500 MiB ext4 partition on the non-encrypted, physical hard drive:
  - Enable `Use Partition`
  - Enable `Format`
  - Use as: `Custom`
  - Custom: `/boot`
  - Filesystem: `Default (ext4)`

Now we unlock the encrypted partition to install elementary OS into it:

8. Click on the encrypted LUKS partition:
  - Password: Enter the previously chosen LUKS password
  - Device name: `elementary`

You should now see a second device in the installer which resembles the previously created LUKS container with its LVM volume(s).

9. Click on the LVM volume:
  - Enable `Use Partition`
  - Use as: `Root (/)`
  - Filesystem: `Default (ext4)`
10. **!! Double Check Everything - any mistakes at this step and you have to start all over !!**
  - Once you are sure everything is correct, click `Erase and install`

After the installation is complete, your computer is restarted. At this point the bootloader (GRUB) should now allow you to choose whether you want to boot elementary OS or Windows:

```
Elementary
Advanced options for Elementary
Windows Boot Manager (on /dev/nvme0n1p1)
UEFI Firmware Settings
```

11. Select Elementary
12. A password prompt should appear, which asks you to `Please unlock disk elementary`
13. Enter the previously chosen LUKS password
14. Complete the Initial Setup of elementary OS

## 5. Enjoy

Congratulations! You successfuly setup dual boot between elementary OS and Windows along with full disk encryption!

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Acknowledgements

Credits go to [Luis Pabon](https://gist.github.com/luispabon) and [Michal Dziekonski](https://gist.github.com/mdziekon) for their work on this fabulous step by step guide: [Ubuntu + Windows 10 dualboot with LUKS encryption](https://gist.github.com/luispabon/db2c9e5f6cc73bb37812a19a40e137bc)
