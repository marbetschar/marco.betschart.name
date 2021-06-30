---
description: Adding hyperlink support to elementary OS text rendering.
---

# Granite HyperTextView

{% hint style="info" %}
If you like my contributions, [**❤️ Sponsor Me**](https://github.com/sponsors/marbetschar). It would mean the world to me!
{% endhint %}

Coming from macOS, I was used to simply click on URI's in any displayed text and jump right where it points to. As simple and obvious this sounds, this tiny little feature is missing in a lot of platforms. Needless to say, I missed it ever since I made the switch.

Earlier this month [Cassidy published a Tweet](https://twitter.com/CassidyJames/status/1404848863395991558), indicating he is missing the very same feature. Thats when it clicked on my end: Time to dedicate some hours for this! As of today, I built a working, reusable implementation: [`Granite.Widgets.HyperTextView`](https://github.com/elementary/granite/pull/507)- which is a drop in replacement for `Gtk.TextView`. This basically means, as a developer, you can replace any GTK TextView in your application with the new Granite Widget and get the aforementioned URI detection and clickability for free - no additional effort needed!

While I'm still ironing out some edge cases together with other elementary OS developers, I do think the current implementation looks promising and will probably make it into elementary OS 6 for general public - so hang tight!

