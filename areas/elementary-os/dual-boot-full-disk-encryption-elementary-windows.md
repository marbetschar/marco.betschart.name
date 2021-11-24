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

# Dual Boot with Full Disk Encryption on elementary OS and Windows

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

### 1.3 Completely Wipe Hard Drive (Optional)

While this step is optional, it is highly recommended to wipe the entire hard drive before starting this setup. This ensures ...

To do so, we boot elementary OS in Demo Mode:

1. Boot from elementary OS USB stick
2. After the installer starts:
   - Select your language
   - Select your keyboard layout
3. On the "Try or Install" step, choose "Try Demo Mode" and confirm

Once elementary OS is booted, start GParted from the Applications Menu.

In GParted:

1. Delete all available partitions
2. Create a new partition which occupies the entire hard disk (just use the default file system)
3. Click "Apply All Operations". You should end up with one partition

In my case the partition device is named `/dev/nvme0n1p1`:

_The new partition which occupies the entire hard disk_

At this point we need to fall back to the Terminal, because GParted is [not able to create encrypted LUKS containers yet](https://gparted.org/features.php).
Open the Terminal and run the following commands:

```bash
# Create a LUKS container ("luksFormat" is case sensitive):
sudo cryptsetup luksFormat /dev/nvme0n1p1

# Open the previously created LUKS container with name 'cryptdrive' ("luksOpen" is case sensitive):
sudo cryptsetup luksOpen /dev/nvme0n1p1 cryptdrive

# Wipe entire cryptdrive by fill it completely with random data (this took about 1h on my 1TB drive):
sudo dd if=/dev/zero of=/dev/mapper/cryptdrive bs=16M

# Close the LUKS container ("luksClose is case sensitive):
sudo cryptsetup luksClose cryptdrive
```

# 2. Partitioning

## 2.1 Boot elementary OS in Demo Mode

Since we are going to create encrypted LUKS containers, we need to boot elementary OS in Demo Mode to do the partitioning:

1. Boot from elementary OS USB stick
2. After the installer starts:
   - Select your language
   - Select your keyboard layout
3. On the "Try or Install" step, choose "Try Demo Mode" and confirm

## 2.2 Create Partitions in GParted

**IMPORTANT:** There's currently no easy way to make grub work with an encrypted partition.
**Make sure `/boot` and `/boot/EFI` are their own partitions and left unencrypted**.

Once elementary OS is booted, start GParted from the Applications Menu. Then in GParted:

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

# 3. Install Windows

**PLEASE NOTE:** Windows was not able to recognize my hard disk during install on a Dell XPS 9310. The solution was to change the storage type from RAID to AHCI/NVMe in the BIOS ([see this Dell community question](https://www.dell.com/community/XPS/Pros-Cons-AHCI-vs-Raid-On-XPS13-9300-NVMe/td-p/7636984) for more information about the different types).

1. Boot from the Windows USB stick
2. Install Windows on the partition you created in step 2.
3. Once Windows is installed you're done with it for now

At this point, you could enable encryption, install additional drivers etc. But I recommend to setup elementary OS first, because if something goes wrong you'll need to start all over again.

# 4. Install elementary OS

...


# Sources

- [XPS 15 9570 - DualBoot with Encryption (Windows 10 with BitLocker + Ubuntu 18.04 with LVM on LUKS)](https://gist.github.com/mdziekon/221bdb597cf32b46c50ffab96dbec08a)