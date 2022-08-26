# OpenXR: Monado

The open source OpenXR runtime.

### Installation

```shell
# Make sure to install the correct vulkan driver for your video card:
sudo pacman -S vulkan-radeon

# Install Monado
yay monado-git

# At the time of this writing the openxr-loader-git package is
# broken due to a python dependency issue. We therefore need to
# workaround it (see https://github.com/pallets/markupsafe/issues/282#issuecomment-1043899655)
#pacman -S python-pip
#pip install -Iv markupsafe==2.0.1

# Install OpenXR Loader
#yay openxr-loader-git
```

### Test

Now as everything is installed now, its time to probe for devices to see whether Monado is capable to detect your hardware. You should see something similar to the output below:

```shell
monado-cli test
:: Creating instance!
:: Probing!
:: Dumping!
...
:: Creating system devices!
 WARN [setup_visual_trackers] No visual trackers were set
ERROR [opengloves_get_bt_devices] Failed to open socket!
ERROR [opengloves_get_bt_devices] Failed to open socket!
ERROR [opengloves_load_config_file] Failed to load config file
 INFO [p_create_system] Creating system:
	Builders:
		rgb_tracking: RGB tracking based devices (PSVR, PSMV, ...)
		lighthouse: Lighthouse-tracked (Vive, Index, Tundra trackers, etc.) devices builder
		remote: Remote simulation devices builder
		legacy: Legacy probing system
	No builder selected in config (or wasn't compiled in)
	Selected lighthouse because it was certain it could create a head
	Using builder lighthouse: Lighthouse-tracked (Vive, Index, Tundra trackers, etc.) devices builder
	Result: XRT_SUCCESS
 :: Listing created devices!
	 0: Valve Index (vive)
	 1: Valve Index Right Controller (vive)
	 2: Valve Index Left Controller (vive)
 :: Listing role assignments!
	head:                Valve Index (vive)
	left:                Valve Index Left Controller (vive)
	right:               Valve Index Right Controller (vive)
	gamepad:             <none>
	hand_tracking.left:  Valve Index Left Controller (vive)
	hand_tracking.right: Valve Index Right Controller (vive)
 :: All ok, shutting down.
 :: Exiting '0'
```

### Run

Everything seems fine, so lets start the monado-service:

```shell
monado-service
# Hit enter to stop it
```