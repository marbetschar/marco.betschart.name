# xrdesktop: wxrd

A prototype-quality standalone client for xrdesktop based on wlroots and the wxrc codebase.

### Requirements

Make sure to first [install an OpenXR compatible runtime such as Monado](openxr-monado.md).

### Build

```shell
# Install required libraries:
sudo pacman -S meson cmake wayland-protocols seatd glew glfw-wayland shaderc xcb-util-errors

# Now we are ready to configure:
mkdir -p ~/Development/xrdesktop
cd ~/Development/xrdesktop
git clone --recursive https://gitlab.freedesktop.org/xrdesktop/wxrd.git
cd wxrd

cd subprojects
git clone https://gitlab.freedesktop.org/xrdesktop/gulkan.git -b next
git clone https://gitlab.freedesktop.org/xrdesktop/gxr.git -b next
git clone https://gitlab.freedesktop.org/xrdesktop/xrdesktop.git -b next
cd ..

# meson >= 0.60 fails with unknown option
# https://github.com/mesonbuild/meson/issues/932#issuecomment-1006155441
meson -Ddefault_library=static build

# It's compilation time. We need install here so wxrd
# is capable to find xrdesktop when run:
ninja -C build install
```

### Run

Make sure [the `monado-service` runs](openxr-monado.md#run) and then execute:

```shell
./build/src/wxrd
```