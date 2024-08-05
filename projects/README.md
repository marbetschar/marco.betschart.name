---
description: a project is a series of tasks linked to a specific goal, with a deadline.
---

# My Projects

The characteristics of a project are:

* **goal** to be achieved
* has a **deadline**

[**Read why the differentiation from areas is important**](../about-this-website.md#why-the-distinction-between-projects-and-areas-is-important)

## My Current Projects

{% hint style="info" %}
If you like my work, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

{% content-ref url="bachelors-degree-in-computer-science.md" %}
[bachelors-degree-in-computer-science.md](bachelors-degree-in-computer-science.md)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="foss-productivity-system.md" %}
[foss-productivity-system.md](foss-productivity-system.md)
{% endcontent-ref %}

{% content-ref url="../archives/projects/progress-for-apple-reminders.md" %}
[progress-for-apple-reminders.md](../archives/projects/progress-for-apple-reminders.md)
{% endcontent-ref %}

{% content-ref url="time-limit.md" %}
[time-limit.md](time-limit.md)
{% endcontent-ref %}

## Project Ideas

Stuff I'd love would already exist and I might work on in the future.

_**A-Z**_

### ASCII-Art drawing tool for elementary OS AppCenter

**Problem**

It would be great to have an offline capable, ASCII-Art drawing tool available through elementary OS AppCenter. This would allow to create simple graphics in a standardized and long-lasting format - which is especially useful for a Zettelkasten.

**Proposal**

There is already a quite good web application called ASCIIFlow which is capable of creating simple ASCII Drawings. It is open source as well, so it would be great to simply re-package it in Flatpak and distribute it through AppCenter for offline usage.

**Prior Art**

* Cassidy already built a [template for embedding a Web-App](https://github.com/cassidyjames/plausible)
* [Monodraw for macOS](https://monodraw.helftone.com/)

### elementary Calendar Weekly View

**Problem**

The elementary OS Calendar App currently only features a monthly view for events. While this works Ok, it is not my preferred way for scheduling. I'd prefer a weekly view, since I tend to schedule weeks in advance and block time slots in my days for specific projects. Therefore it is crucial for me to see the available hours per day.

**Proposal**

The WeekView is not trivial to implement, since it needs to consider a lot of local factors such as LTR/RTL, timezones, start day of week (Sunday vs. Monday) etc. It also needs to support draggability in order to be actually useful.

But still: It is worth the effort, because I miss this view each and every day.

**Prior Art**

* There have been [several requests and attempts](https://github.com/elementary/calendar/issues/500) to add this feature to Calendar.

### Jupyter Notebook as elementary OS Desktop App

**Problem**

Installing and using Jupyter Notebook on the Linux Desktop feels a bit clunky: All happens on the command line - although Jupyter itself is GUI oriented. I'd love to have better desktop integration - even just a start menu icon which automatically starts the server and a browser which points at the right URL would be a massive improvement.

**Proposal**

The best thing would be to have an pre-packaged Jupyter Notebook app in the elementary AppCenter, which installs everything needed. As GUI we probably can use a Gtk web wrapper, similar to the way Cassidy did it in [his Plausibe app for elementary OS](https://github.com/cassidyjames/plausible). We probably also want to [adjust the default Jupyter Notebook GUI](http://christopherroach.com/articles/jupyterlab-desktop-app/), so it provides a more integrated experience on the Desktop. Of course, starting/stopping the desktop GUI should automatically take care of starting/stopping the Jupyter Notebook server.

**Prior Art**

* [Official documentation](http://jupyterlab.io/install)
* [Running Jupyter Lab as a Desktop Application](http://christopherroach.com/articles/jupyterlab-desktop-app/)
* [Cassidy's Plausibe Web UI Gtk Wrapper](https://github.com/cassidyjames/plausible)
* [Juno - Jupyter Notebook IDE for iOS](https://apps.apple.com/us/app/juno/id1462586500)

### KDE Connect for elementary OS

**Problem**

There should be a native way to securely connect to mobile devices and other desktops to:

* Share files, links and text
* Send and receive messages
* Sync clipboard content
* Sync contacts
* Sync notifications
* Control media players
* Control system volume
* Execute predefined commands
* And more…

**Proposal**

To achieve this, we can add native support for KDE Connect to elementary OS. This probably means to add plugins in Files, Wingpanel, System Settings and other core components of elementary OS.

**Prior Art**

* [KDE Connect Support #338](https://github.com/elementary/wingpanel/issues/338)
* [Conecto - a GTK client for KDEConnect](https://github.com/hannesschulze/conecto/)
* [mconnect](https://github.com/bboozzoo/mconnect)
* [GSConnect](https://github.com/GSConnect/gnome-shell-extension-gsconnect)
* [KDE Connect](https://kdeconnect.kde.org/)
* [KDE Connect Indicator](https://github.com/b4j4/indicator-kdeconnect)
