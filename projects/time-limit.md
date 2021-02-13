---
description: |
  A simple and beautiful timer app for elementary OS
---

# Time Limit


# <img src=".gitbook/assets/com.github.marbetschar.time-limit.png" align="left" /> Time Limit

## Usage

Drag the blue arrow to set a timer. Release to start and click to pause.
When the time is up, a notification will show up with a nice sound.

### Keyboard shortcuts

- `Space` for pause/play
- `Esc` to reset

## Installation

[![Get it on AppCenter](https://appcenter.elementary.io/badge.svg)](https://appcenter.elementary.io/com.github.marbetschar.time-limit)

## Building

You'll need the following dependencies:
* glib-2.0
* gtk+-3.0
* granite >=0.5
* unity
* meson
* valac

Simply run

```
./install.sh
```

The install script configures the build environment, compiles the app and installs it.
The app is started automatically after successful installation.

## Acknowledgements

- Designed by [Michael Villar](https://github.com/michaelvillar/timer-app).