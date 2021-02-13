---
description: How to fix could not find a distribution template for Elementary/odin when executing add-apt-repository.
tags: [workaround, elementary, troubleshooting, linux-desktop]
---

# Fix Error: could not find a distribution template for Elementary/odin

![elementary OS: 6 Odin](https://img.shields.io/badge/elementary%C2%A0OS-6%20Odin-007aff)
![Status: Verified](https://img.shields.io/badge/status-verified-green.svg)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me on GitHub**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

You might encounter the following error during execution of `add-apt-repository`:

> Traceback \(most recent call last\): File "/usr/bin/add-apt-repository", line 108, in sp = SoftwareProperties\(options=options\) File "/usr/lib/python3/dist-packages/softwareproperties/SoftwareProperties.py", line 118, in **init** self.reload\_sourceslist\(\) File "/usr/lib/python3/dist-packages/softwareproperties/SoftwareProperties.py", line 613, in reload\_sourceslist self.distro.get\_sources\(self.sourceslist\)  
> File "/usr/lib/python3/dist-packages/aptsources/distro.py", line 91, in get\_sources raise NoDistroTemplateException\( aptsources.distro.NoDistroTemplateException: Error: could not find a distribution template for Elementary/odin

This error is due to the pre-release nature of elementary 6.0 Odin and should be fixed once the stable version is released. Meanwhile you can [apply the existing workaround](https://github.com/elementary/os-patches/issues/136#issuecomment-698652540):

_Edit `sudo vi /etc/lsb-release`:_

```diff
-DISTRIB_ID=elementary
-DISTRIB_RELEASE=6
-DISTRIB_CODENAME=odin
-DISTRIB_DESCRIPTION="elementary OS 6 Early Access"
+DISTRIB_ID=Ubuntu
+DISTRIB_RELEASE=20.04
+DISTRIB_CODENAME=focal
+DISTRIB_DESCRIPTION="Ubuntu 20.04.1 LTS"
```

_Edit `sudo vi /etc/os-release`:_

```diff
-NAME="elementary OS"
-VERSION="6 Early Access"
-ID=elementary
-ID_LIKE=ubuntu
-PRETTY_NAME="elementary OS 6 Early Access"
-LOGO=distributor-logo
-VERSION_ID="6"
-HOME_URL="https://elementary.io/"
-DOCUMENTATION_URL="https://elementary.io/docs/learning-the-basics"
-SUPPORT_URL="https://elementary.io/support"
-BUG_REPORT_URL="https://github.com/elementary/os/issues/new"
-PRIVACY_POLICY_URL="https://elementary.io/privacy-policy"
-VERSION_CODENAME=odin
-UBUNTU_CODENAME=focal
+NAME="Ubuntu"
+VERSION="20.04.1 LTS (Focal Fossa)"
+ID=ubuntu
+ID_LIKE=debian
+PRETTY_NAME="Ubuntu 20.04.1 LTS"
+VERSION_ID="20.04"
+HOME_URL="https://www.ubuntu.com/"
+SUPPORT_URL="https://help.ubuntu.com/"
+BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
+PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
+VERSION_CODENAME=focal
+UBUNTU_CODENAME=focal
```

After you changed both files, try to execute `add-apt-repository` again.