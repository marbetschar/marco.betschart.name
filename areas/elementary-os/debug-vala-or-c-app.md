---
description: How to effectively debug Vala or C code.
tags:
  - how-to
  - open-source
  - vala
  - c
  - debug
  - development
---

# Debug a Vala or C App

> ![elementary OS: 6.0 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff)
> ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="warning" %}
This page mainly focuses on debugging in the Terminal. If you want to setup a graphical environment for Vala development and debugging,
please have a look at [**Vala Development in VSCode**](../../resources/linux-desktop/vscode-vala-development.md).
{% endhint %}

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Enable Debug Output

Set the environment variable `G_MESSAGES_DEBUG` to `all` to get all log messages printed to stdout:

```bash
export G_MESSAGES_DEBUG=all
```

## Using GNU Debugger

### Installing GNU Debugger

```bash
sudo apt install gdb
```

### Retrieve a backtrace \(e.g. to debug a Segmentation fault\)

Run the program in question with GNU Debugger:

```bash
$ gdb /path/to/executable
...
Reading symbols from /path/to/executable...
(gdb) run
```

Once the application crashes you should see a message similar to the following:

```bash
Thread 1 "executable" received signal SIGSEGV, Segmentation fault.
0x00007ffff709b434 in my_function_in_which_the_code_crashed () from /lib/x86_64-linux-gnu/libxyz-1.6.so.62
(gdb)
```

To retrieve a backtrace at this state, simply execute the `backtrace` command:

```bash
(gdb) backtrace
#0  0x00007ffff709b434 in my_function_in_which_the_code_crashed () at /lib/x86_64-linux-gnu/libxyz-1.6.so.62
#1  0x00005555555962ef in my_previously_executed_function (node=0x7fffffffcbc0, highest=1537725293) at ../src/MyCode/UsefulStuff.vala:168
...
(gdb) quit
```

### Retrieve a backtrace for a warning or critical message

In this case you want to abort the program as soon as a warning or critical message is logged. To do so, the `G_DEBUG` environment variable comes in handy:

```bash
# Causes GLib to abort the program at the first call to g_warning()
# or g_critical(). Use of this flag is not recommended except when
# debugging:
export G_DEBUG=fatal-warnings

# Causes GLib to abort the program at the first call to g_critical().
# This flag can be useful during debugging and testing:
export G_DEBUG=fatal-criticals
```

Once the environment variable is set, it causes the application to crash at the desired place. You are then able to retrieve a backtrace as described above.

## Using core dumps

You can let Linux automatically collect the required information for a backtrace whenever an application crashes unexpectedly. This information is stored in a so called "core dump" file which contains the recorded state of the complete memory from the crashed application. Those core dumps are especially useful for errors which occur seemingly at random, because you don't need to explicitly start the application using GNU Debugger and you are still able to retrieve a backtrace after a crash.

{% hint style="info" %}
Please be aware that core dumps **may contain sensitive information** due to their very nature: They are really just a copy of the app's memory at a given point in time. This may or may not include sensitive information such as passwords etc.
{% endhint %}

### Installing systemd-coredump

```bash
sudo apt install systemd-coredump
```

### List existing core dumps

```bash
$ sudo coredumpctl list
TIME                            PID   UID   GID SIG COREFILE  EXE
Fri 2021-05-14 18:57:59 CEST 181233  1000  1000  11 missing   /path/to/executable
Sun 2021-05-16 15:03:01 CEST   3258  1000  1000  11 present   /path/to/other-executable
Mon 2021-05-17 17:23:30 CEST  61215  1000  1000  11 present   /path/to/executable
```

### Debug existing core dump

```bash
$ sudo coredumpctl debug /path/to/executable
...
(gdb) backtrace
#0  0x00007ffff709b434 in my_function_in_which_the_code_crashed () at /lib/x86_64-linux-gnu/libxyz-1.6.so.62
#1  0x00005555555962ef in my_previously_executed_function (node=0x7fffffffcbc0, highest=1537725293) at ../src/MyCode/UsefulStuff.vala:168
...
(gdb) quit
```

## Further Reading

* [Running and debugging GLib Applications](https://developer.gnome.org/glib/stable/glib-running.html)

