# xrdesktop: wxrd

A prototype-quality standalone client for xrdesktop based on wlroots and the wxrc codebase.

### Requirements

Make sure to first [install an OpenXR compatible runtime such as Monado](openxr-monado).

### Build

```shell
# Install required libraries:
pacman -S wayland-protocols seatd glew

# gxr compilation fails if gulkan is not already present
# therefore we install gulkan's `next` branch from AUR:
yay --editmenu gulkan-git
1 aur/gulkan-git 0.15.1.300.f39526a-1 (+3 0.11) 
    A GLib library for Vulkan abstraction.
==> Packages to install (eg: 1 2 3, 1-3 or ^4)
==> 1
...
==> PKGBUILDs to edit?
==> [N]one [A]ll [Ab]ort [I]nstalled [No]tInstalled or (1 2 3, 1-3, ^4)
==> A
...
source=('git+https://gitlab.freedesktop.org/xrdesktop/gulkan.git#branch=next')
...
==> Proceed with install? [Y/n] Y

# Now we are ready to configure:
mkdir -p ~/Development/xrdesktop
cd ~/Development/xrdesktop
git clone --recursive https://gitlab.freedesktop.org/xrdesktop/wxrd.git
cd wxrd

cd subprojects
git clone https://gitlab.freedesktop.org/xrdesktop/gxr.git -b next
git clone https://gitlab.freedesktop.org/xrdesktop/xrdesktop.git -b next
cd ..

# meson >= 0.60 fails with unknown option
# https://github.com/mesonbuild/meson/issues/932#issuecomment-1006155441
meson -Ddefault_library=static build

# It's compilation time:
ninja -C build
```

### Run

Make sure [the `monado-service` runs](openxr-monado.md#run) and then execute:

```shell
./build/src/wxrd
```