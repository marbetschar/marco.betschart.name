---
description: How to convert ACSM file to a DRM free ePub
---

# Convert Kobo ACSM to DRM free ePub

> ![elementary OS: 5.1 Hera](https://img.shields.io/badge/elementary%C2%A0OS-5.1%20Hera-007aff)
> ![Status: Verified](https://img.shields.io/badge/status-verified-58c633)

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

## Install Knock

Go to the [knock project on GitHub](https://github.com/BentonEdmondson/knock) and install the latest version as described there:

```
cd ~/Downloads
mv knock-* knock
chmod +x knock
```

## Download the ACSM file from Kobo

Head over to the Kobo website and download the previously purchased book. Your browser will download a file stored at `~/Downloads/URLLink` (without extension) which is essentially the book's ACSM file.

## Convert the ACSM file to a DRM free ePub

Now let `knock` do the download and the conversion:

```
$ cd ~/Downloads
$ ./knock ./URLLink
downloading the file from Adobe...
Download 100%
removing DRM from the file...
DRM-free EPUB file generated at .epub
$ mv .epub Book.epub
```

**And that's it: You now own a DRM free copy of your purchased book!**
