---
description: 'a project is a series of tasks linked to a specific goal, with a deadline.'
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

{% page-ref page="bachelors-degree-in-computer-science.md" %}

{% page-ref page="elementary-mail-v2.0.md" %}

{% page-ref page="elementary-tasks-v1.0.md" %}

{% page-ref page="elementary-xrdesktop-support.md" %}

{% page-ref page="progress-for-apple-reminders.md" %}

{% page-ref page="time-limit.md" %}

## Project Ideas

Stuff I'd love would already exist and I might work on in the future.

### elementary OS

#### Jupyter Notebook as Desktop App

**Problem**

Installing and using Jupyter Notebook on the Linux Desktop feels a bit clunky: All happens on the command line - although Jupyter itself is GUI oriented. I'd love to have better desktop integration - even just a start menu icon which automatically starts the server and a browser which points at the right URL would be a massive improvement.

**Proposal**

The best thing would be to have an pre-packaged Jupyter Notebook app in the elementary AppCenter, which installs everything needed. As GUI we probably can use a Gtk web wrapper, similar to the way Cassidy did it in [his Plausibe app for elementary OS](https://github.com/cassidyjames/plausible). We probably also want to [adjust the default Jupyter Notebook GUI](http://christopherroach.com/articles/jupyterlab-desktop-app/), so it provides a more integrated experience on the Desktop. Of course, starting/stopping the desktop GUI should automatically take care of starting/stopping the Jupyter Notebook server.

**Prior Art**

- [Official documentation](http://jupyterlab.io/install)
- [Running Jupyter Lab as a Desktop Application](http://christopherroach.com/articles/jupyterlab-desktop-app/)
- [Cassidy's Plausibe Web UI Gtk Wrapper](https://github.com/cassidyjames/plausible)
- [Juno - Jupyter Notebook IDE for iOS](https://apps.apple.com/us/app/juno/id1462586500)