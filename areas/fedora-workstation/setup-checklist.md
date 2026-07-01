---
description: My personal checklist for setting up a fresh Fedora Workstation installation.
---

# Setup Checklist

Tested on Fedora Workstation 44, RTX 5060 Ti eGPU, ThinkPad X1 Yoga

## Base System Fedora Everything 44

1. [Download Fedora Everything 44](https://fedoraproject.org/misc/#minimal)
2. **Install**:
   - Select **"Fedora Custom Operation System"**
     - AND **Common NetworkManager Submodules**
     - AND **Standard** (common set of utilities)
   - **Partitioning**: Use automatic (Btrfs)
   - **User**: Create your account with `sudo` access

## Fix Wifi

```bash
nmcli device status
```

In case this does not list the WiFi device, connect your Hotspot via USB Tethering and run the following commands:

```bash
wget https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/plain/intel/iwlwifi/iwlwifi-so-a0-gf-a0-89.ucode
wget https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/plain/intel/iwlwifi/iwlwifi-so-a0-gf-a0.pnvm

sudo mv iwlwifi-so-* /lib/firmware/

sudo chown root:root /lib/firmware/iwlwifi-so-*
sudo chmod 644 /lib/firmware/iwlwifi-so-*

sudo modprobe -r iwlwifi
sudo modprobe iwlwifi
````

Then, check again and connect to your WLAN:

```bash
nmcli device status
nmcli device wifi connect <SSID> --ask
```

## Install Desktop

After first boot, run the following commands on the command line:

```bash
sudo dnf install niri niri-settings
sudo dnf install --nogpgcheck --repofrompath 'terra,https://repos.fyralabs.com/terra$releasever' terra-release
sudo dnf install noctalia-shell
sudo dnf install noctalia-greeter
```

Start Noctalia from Niri:

```
# ~/.config/niri/config.kdl:
spawn-at-startup "qs" "-c" "noctalia-shell"
```

Then make sure to configure greetd:

```
# /etc/greetd/config.toml:
[terminal]
vt = 1

[default_session]
command = "env XKB_DEFAULT_LAYOUT=ch /usr/bin/noctalia-greeter-session"
user = "greetd"
```

And finally boot into your lightweight Niri + Noctalia desktop:

```bash
sudo systemctl set-default graphical.target
sudo systemctl enable greetd --now
```

---

4. 
   
   sudo dnf update -y
   sudo dnf install -y git curl wget flatpak
   flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
   ```

## Install Niri

```bash
sudo dnf install -y niri niri-settings
```

## Install Noctalia

```bash
# Add Terra repo (Fyra Labs)
sudo dnf install -y --nogpgcheck --repofrompath='terra,https://repos.fyralabs.com/terra$releasever' terra-release

# Install Noctalia + Quickshell (dependency)
sudo dnf install -y noctalia-shell quickshell
```


## Install NVIDIA Proprietary Drivers

```bash
# Enable RPM Fusion (non-free for NVIDIA)
sudo dnf install -y https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf groupupdate -y "NVIDIA CUDA Toolkit"  # Optional for AI/ML

# Install NVIDIA drivers + CUDA (for RTX 5060 Ti)
sudo dnf install -y akmod-nvidia xorg-x11-drv-nvidia-cuda

# Rebuild initramfs and load kernel module
sudo akmods --force
sudo dracut --force
sudo modprobe nvidia
```

**Verify driver install**:

```bash
nvidia-smi  # Should show your RTX 5060 Ti
glxinfo | grep "OpenGL renderer"  # Should show NVIDIA
```


## Enable Kernel Modesetting (Critical for Wayland)

```bash
sudo grubby --update-kernel=ALL --args="nvidia-drm.modeset=1"
```

**Reboot now** to apply:

```bash
sudo systemctl reboot
```




## Configure Niri to Launch Noctalia

1. **Create config directory**:
   ```bash
   mkdir -p ~/.config/niri
   ```
2. **Edit `~/.config/niri/config.kdl`**:
   ```bash
   cat > ~/.config/niri/config.kdl <<EOF
   # Niri base config
   ...

   # Launch Noctalia (Quickshell component)
   spawn-at-startup "qs" "-c" "noctalia-shell"

   # Required for portals (screenshots, file dialogs, etc.)
   spawn-at-startup "dbus-update-activation-environment" "--systemd" "WAYLAND_DISPLAY" "XDG_CURRENT_DESKTOP=niri"

   # Optional: Enable animations
   animation {
       enable true
   }
   EOF
   ```
3. **Create environment file** (`~/.config/niri/environment`):
   ```bash
   cat > ~/.config/niri/environment <<EOF
   # Ensure Wayland works with NVIDIA
   export NVIDIA_DRM_MODESET=1
   export XDG_SESSION_TYPE=wayland
   export XDG_CURRENT_DESKTOP=niri
   export QT_QPA_PLATFORM=wayland
   export SDL_VIDEODRIVER=wayland
   export CLUTTER_BACKEND=wayland
   EOF
   ```

## Set Up Display Manager (GDM)

1. **Create a custom session for Niri + Noctalia**:
   ```bash
   sudo tee /usr/share/xsessions/niri-noctalia.desktop <<EOF
   [Desktop Entry]
   Name=Niri + Noctalia
   Comment=Scrollable-tiling Wayland compositor with Noctalia shell
   Exec=/usr/bin/niri
   Type=Application
   DesktopNames=Niri
   EOF
   ```
2. **Disable GNOME’s Wayland session** (to avoid confusion):
   ```bash
   sudo mv /usr/share/xsessions/gnome-wayland.desktop /usr/share/xsessions/gnome-wayland.desktop.bak
   ```
3. **Reboot and select "Niri + Noctalia"** at the GDM login screen.


## Thunderbolt eGPU Setup

1. **Install Thunderbolt tools**:
   ```bash
   sudo dnf install -y bolt
   ```
2. **Authorize your eGPU enclosure** (run after first plug-in):
   ```bash
   sudo boltctl authorize <device-UUID>  # List devices with `boltctl list`
   ```
3. **Enable persistent authorization** (so it remembers your eGPU):
   ```bash
   sudo boltctl enroll
   ```

## Post-Install Checks

### Verify Wayland Session
```bash
echo $XDG_SESSION_TYPE  # Should output "wayland"
echo $XDG_CURRENT_DESKTOP  # Should output "niri"
```

### Test NVIDIA eGPU Detection

```bash
lspci | grep -i nvidia  # Should show your RTX 5060 Ti
nvidia-smi             # Should show GPU info (may take ~10-30 sec after plugging in)
```

### Test Noctalia

- Right-click on the desktop → Should show Noctalia’s context menu.
- Press `Super` (Windows key) → Should open the application launcher.

## Troubleshooting

### Black Screen on Login?
1. **Check kernel modesetting**:
   ```bash
   cat /proc/cmdline | grep nvidia-drm.modeset=1
   ```
   If missing, reapply Step 3 and reboot.

2. **Fallback to TTY**:
   - Press `Ctrl+Alt+F2` to switch to a TTY.
   - Run `sudo journalctl -u gdm -b` to check GDM logs.

### Noctalia Doesn’t Launch?
1. **Check Niri logs**:
   ```bash
   journalctl -u niri -f
   ```
2. **Manually test Noctalia**:
   ```bash
   qs -c noctalia-shell
   ```
   If this works, your Niri config is misconfigured.

### eGPU Not Detected?
1. **Check Thunderbolt**:
   ```bash
   boltctl list
   ```
   If unauthorized, run `sudo boltctl authorize <UUID>`.

2. **Check PCIe**:
   ```bash
   lspci | grep -i nvidia
   ```
   If missing, your eGPU may need to be plugged in **before boot**.

## Final Notes

### Hotplug Behavior
- **Plugging in**: Works for **compute-only** (CUDA) after ~10-30 sec (no relogin).
- **Display output**: Requires **relogin** (NVIDIA driver limitation).
- **Unplugging**: Stop all CUDA processes first (`killall python`), then unplug.

### Performance Tips
- **Disable vsync** in Noctalia settings for smoother animations.
- **Use `nvidia-smi -pl 100`** to unlock power limits for AI workloads.
