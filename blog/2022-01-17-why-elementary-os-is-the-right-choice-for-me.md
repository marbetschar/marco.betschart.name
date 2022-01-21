---
description: >-
  A few days ago I was asked on Twitter why I like elementary OS - and here is
  why!
---

# Why elementary OS is the right choice for me

_January 2022_

A few days ago [@MarkKour asked me on Twitter](https://twitter.com/MarkKour/status/1481970455267487746), why I like elementary OS. Because the answer is hard to condense into a handful of Tweets, I decided to write this blog post.

{% hint style="warning" %}
**Be Aware:** The statements below represent my own personal opinion. They neither reflect an official point of view of elementary nor anyone else.
{% endhint %}

## Philosophical Reasons

_Things I like about the self-perception of elementary and how it guides its decisions._

![elementary OS wallpaper by Tj Holowaychuk](../.gitbook/assets/tj-holowaychuk.jpg)

### Community and Communication

The elementary team does a great job of keeping the community in the loop by publishing a summary of each month's updates on [their blog](https://blog.elementary.io). Those summaries are a joy to read because they are very well written and full of screenshots of the improvements described.

In my experience, everything around elementary and its team is very open and forthcoming. Whenever I reached out with a question, I received a helpful answer and if things weren't obvious the team truly tried to understand the matter before jumping to conclusions.

In my opinion this way of communication and the urge to truly understand the motivation _behind_ a request is what makes the difference. Therefore, [getting involved](https://elementary.io/get-involved) is a lot of fun and rewarding as well.

### Design is neither an add-on nor an opinion

The [elementary Design Philosophy](https://docs.elementary.io/hig/design-philosophy) is right on point: Design is something deeply integrated in whatever you create. Its the sum of all the tiny little decisions. Its not something you can start to think of at the very end - and the effectiveness of a design is measurable: If the problem is well understood, then the effectiveness of different designs can objectively be compared.

And here we come full circle now: As mentioned, the community and communication all around elementary is all about understanding the specific problem at hand - always with the goal in mind to find the best possible solution.

This whole approach really shows in the overall User Experience (UX) of elementary OS. For example [Accessibility Features Are Just Features](https://blog.elementary.io/accessibility-features-are-just-features/). Or another very nice example is the elementary OS installer: [It offers to switch to a left-handed setup if the users clicks on the `Next` button with the right mouse button](https://github.com/elementary/initial-setup/pull/133):

![eOS installer offers to switch to left-handed setup](<../.gitbook/assets/eOS-installer-offers-to-switch-to-left-handed-setup (1).gif>)

Some other things I really like in terms of UX in elementary OS are [Multi Touch Gestures](https://blog.elementary.io/multitouch-gestures-in-elementary-os-6/) and the [Dark Style](https://blog.elementary.io/dark-style-progress/).

### Open Source does not imply Free Labor

Open Source does not force you into a [Walled Garden](https://www.techtarget.com/searchsecurity/definition/walled-garden), does not see [you as the product](https://blog.elementary.io/you-are-not-the-product/) and on top of that, Open Source allows you to change it however pleases you. Consequently, you need access to the actual source
code of a program, otherwise you can't change it.

And here comes the catch: A lot of people tend to ignore that Open Source is not about getting source code for free. It is about freedom. And the foundation of this freedom is not built on love alone - it's built on human labor.

That's why I really like the Pay-What-You-Can pricing model of elementary and its [AppCenter](https://appcenter.elementary.io): It makes the labor involved far more prominent and at the same time its much easier to send a few bucks of appreciation.

You are now probably thinking about Walled Gardens. But before you are jumping to conclusions, you need to know that AppCenter is not limited to elementary OS! The [AppCenter for Everyone initiative](https://www.indiegogo.com/projects/appcenter-for-everyone/#/) launched by the elementary team itself enables AppCenter on other Linux distributions as well.

{% embed url="https://twitter.com/elementary/status/1482104137961508864" %}
AppCenter for Everyone: elementary Apps can be installed on other Linux distributions as well
{% endembed %}

### Privacy

Let's face it: The whole privacy discussion boils down to one thing - and that's trust. If you are working with some proprietary platform and trust it to not share your data with an unwanted party, that's fine. But you shouldn't be too surprised if your trust is unjustified: At the end of the day the proprietary platform exists in a profit-oriented world and its hard to keep such a platform accountable solely based on its marketing claims.

Therefore, I [neither want to be the product](https://blog.elementary.io/you-are-not-the-product/), [nor share private data with anyone I'm not fully aware of](https://blog.elementary.io/privacy-and-elementary-os/). So choosing elementary OS in terms of privacy was a no-brainer for me.

## Technical Reasons

_Technical decisions made by the elementary OS team are in line with my personal needs._

![elementary OS wallpaper by SpaceX](../.gitbook/assets/photo-by-space-x.jpg)

### Based on Ubuntu LTS: A stable, widely used low maintenance foundation

elementary OS builds on the latest [Ubuntu LTS (Long Term Support)](https://ubuntu.com/blog/what-is-an-ubuntu-lts-release). This basically means the foundation of elementary OS is guaranteed to receive bug fixes and security updates for years to come. Because all of these are well tested, elementary OS is a highly stable computing platform which needs very low maintenance effort.

And just in case things go wrong at some point: Ubuntu is widely used - so there is a huge community to reach out for help.

### Flatpak: App Sandboxing

Even though the classic package format (`*.deb`) is fine for software management on operating system level, it comes with some downsides when used for desktop applications:

**Problem 1: Security**

`*.deb` packages are always installed by `root` (the Administrator of Linux), but the ultimate actions triggered during installation are defined by the package itself. This basically means, each time you install, update or remove a `*.deb` package you give it full access and therefore full control over your entire hard drive with all data stored on it. Unfortunately there is no way to mitigate this, because it is not possible to install, update or remove a `*.deb` package as a regular user.

**Problem 2: Freshness**

Being able to install the latest version of each application using a traditional package format such as `*.deb` is difficult, because this format relies on shared libraries and binaries provided by the underlying operating system. If the underlying operating system gets older, the provided versions of the shared libraries and binaries may no longer be compatible with the latest version of the desktop application. Therefore, keeping everything in sync gets harder and harder over time.

**Solution: App Sandboxing**

Flatpak solves these issues by providing a package format which allows the developer to shield its app from the surrounding operating system. This mechanism is called sandboxing. Since the app now lives within a sandbox, the developer can also add all additionally needed libraries and binaries to the app's sandbox and therefore increase the apps portability.

But the sandbox does not only protect the app from unsupported library versions, it also works the other way around: The sandbox does not allow the app to access surrounding operating system resources - unless explicitly granted by the user. This includes hard drive access as well as access to other hardware such as webcams or microphones.

Last but not least, Flatpak also allows to install, update or remove an app for one specific user only. So there is no `root` permission needed to manage applications.

If you want to know more, make sure to read the [Flatpak article on the elementary blog](https://blog.elementary.io/elementary-appcenter-flatpak/).

**Why is this relevant?**

Traditionally in the Linux world, I had to make a choice: Either I want to be able to use the latest available software - or I'm fine with older versions which are better tested and therefore more stable. This choice not only affects desktop software, it affects the entire operating system. Or to put it bluntly: You had to choose between brand new, unstable distributions with potential high risk of breakage or older, better tested and therefore lower risk distributions.

The first option is good for developers and tinkerers, the second option is a solid choice for servers. But for an everyday user which needs access to new features but does not want to compromise on stability? Both are bad.

That's why I love elementary OS' unique approach: The foundation is built using the highly stable low maintenance Ubuntu LTS release. This means it is well tested and I don't have to worry about it. But at the same time, I can use the latest and greatest desktop applications which may require newer libraries - which are shipped within their own sandbox thanks to Flatpak. So both approaches can coexist and complement each other.

### Documentation

As a developer coming from macOS, I was spoiled by the Apple ecosystem. Especially in terms of its documentation: Design best practices (Human Interface Guidelines), development, release processes and programming API's - everything is documented and a lot of examples are provided.

So I was very pleased to find elementary OS does a marvelous job in terms of documentation too. Their documentation really helps getting involved: They provide a [developer welcome page](https://developer.elementary.io), [design best practices (Human Interface Guidelines)](https://docs.elementary.io/hig/), [development and release process documentation](https://docs.elementary.io/develop/) and a [documentation for programming API's](https://valadoc.org) as well. On top of all that, in case you want to contribute to the operating system itself, there is even a [Contributor Guide](https://docs.elementary.io/contributor-guide/) which helps you to get started with this as well.

## Final Thoughts

![elementary OS wallpaper by Julia Craice](../.gitbook/assets/julia-craice.jpg)

In case you are thinking to switch to elementary OS: Try to give it a fair chance by getting used to the way elementary OS does things. You would not expect macOS to work the same way as Windows, right? Each platform has its own characteristics. Getting acustomed to a new platform takes some time. And if its not for you, that's fine - but it does not make it a bad platform.

Don't get me wrong: As with any software out there, elementary OS is by no means perfect. There are things which - I think - are still [missing or need some annoying workarounds](https://www.marco.betschart.name/areas/elementary-os/missing-features-and-workarounds). You'll probably find some quirks yourself as well.

And if that's the case, it would be great to [get you involved too](https://elementary.io/get-involved)! As mentioned before its a lot of fun working with the elementary team and seeing your own contributions released to the world is just awesome! The beautiful side effect: It makes elementary OS better for all of us!

Last but not least: In case you are currently using macOS and thinking about taking the leap, make sure to read the 5-part series written by [@CassidyJames](https://twitter.com/CassidyJames) on the elementary blog about…

**Switching from macOS:**

1. [The Basics](https://blog.elementary.io/switching-from-macos-the-basics/)
2. [Developer Environment](https://blog.elementary.io/switching-from-macos-developer-environment/)
3. [Creative Work](https://blog.elementary.io/switching-from-macos-creative-work/)
4. [Hardware](https://blog.elementary.io/switching-from-macos-hardware/)
5. [Open Source](https://blog.elementary.io/switching-from-macos-open-source/)
