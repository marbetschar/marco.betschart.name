---
tags:
  - how-to
  - elementary
  - vala
  - vscode
  - programming
  - linux-desktop
description: How to setup VSCodium (Open Source Visual Studio Code) for Vala development.
---

# VSCode: Vala Development

> <img src="https://img.shields.io/badge/elementary%C2%A0OS-6.0%20Odin-007aff" alt="elementary OS: 6.0 Odin" data-size="original"><img src="https://img.shields.io/badge/status-verified-58c633" alt="Status: Verified" data-size="original">

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## VSCodium

_Install VSCodium from deb package (as documented on_ [_the official website_](https://vscodium.com/#install)_)._

Add the GPG key of the repository:

```bash
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | gpg --dearmor | sudo dd of=/etc/apt/trusted.gpg.d/vscodium.gpg
```

Add the repository:

```bash
echo 'deb https://paulcarroty.gitlab.io/vscodium-deb-rpm-repo/debs/ vscodium main' | sudo tee --append /etc/apt/sources.list.d/vscodium.list
```

Update package information and install vscodium:

```bash
sudo apt update && sudo apt install codium
```

## Syntax Highlighting

To begin with, you need to install the [Vala Plugin for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=prince781.vala):

1. Visit the [plugin's website](https://marketplace.visualstudio.com/items?itemName=prince781.vala) and click "Download Extension" (a \*.vsix file)
2. Run VSCodium
3. From within VSCodium, open the Extensions tab (`Ctrl + Shift + X`)
4. Click `... > Install from VSIX...` on top of the Extensions sidebar
5. Select the previously downloaded \*.vsix file and click `Install`

Now you can install the [Vala Language Server](https://github.com/benwaffle/vala-language-server). For this, open a Terminal and execute the following command:

```bash
sudo apt install vala-language-server
```

## Debugging

Install the [CodeLLDB Plugin for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb):

1. Visit the [plugin's website](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb) and click "Download Extension" (a \*.vsix file)
2. Run VSCodium
3. From within VSCodium, open the Extensions tab (`Ctrl + Shift + X`)
4. Click `... > Install from VSIX...` on top of the Extensions sidebar
5. Select the previously downloaded \*.vsix file and click `Install`

Now you can install the [LLDB Debugger](https://lldb.llvm.org/). For this, open a Terminal and execute the following command:

```bash
sudo apt install lldb
```

Make sure to restart VSCodium and then you are nearly ready to start: When you start the debugger the first time in a project, it will ask for a run configuration. Here's a minimal one which should be enough to get you started:

```json
{
  "version": "0.2.0",
  "configurations": [{
    "type": "lldb",
    "request": "launch",
    "name": "Debug",
    "program": "${workspaceFolder}/build/src/com.github.myteam.myapp",
    "args": [],
    "cwd": "${workspaceFolder}"
  }]
}
```

If you want to know more, make sure to have a look at the [README in the CodeLLDB repo](https://github.com/vadimcn/vscode-lldb).

## Further Reading

* [VSCodium: Open Source Binaries of VSCode](https://vscodium.com/)
* [Vala Plugin for Visual Studio Code](https://github.com/prince781/vala-vscode)
* [CodeLLDB Plugin for Visual Studio Code](https://github.com/vadimcn/vscode-lldb)
* [Vala Language Server on GitHub](https://github.com/benwaffle/vala-language-server)
* [How To Add PPA Repository Manually Without "add-apt-repository" On Ubuntu](https://blog.zackad.dev/en/2017/08/17/add-ppa-simple-way.html)
