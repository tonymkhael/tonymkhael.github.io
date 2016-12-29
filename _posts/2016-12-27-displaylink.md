---
layout: post
title:  "DisplayLink & Windows: A terrible adventure"
date:   2016-12-27 12:34:2 +0100
categories: system
tags: DisplayLink Windows Acer WUDFHost.exe performance
excerpt_separator: <!--more-->
---

I'll show you how to setup your USB monitor in replace mode, using a very hacky trick to avoid having the usb driver
drain all of your cpu resources.

<!--more-->

# A solution to which problem?

If you find yourself in the following conditions, the solution presented below is adapted for you:

1. You have a USB monitor that you want to use in replace mode i.e. as your main display, instead of your laptop's.
2. Your PC is running a recent build of windows 10.
3. Having (1 & 2), some `WUDFHOST.exe` process is constantly draining your CPU resources (40%).

First, let me tell you what this process is, and why it is draining so much CPU.

* `WUDFHOST.exe` is a windows generic process that hosts driver code, i.e. the thing that makes use of your hardware, and your USB
monitor in the described circumstances.
* The reason why this driver is consuming so much of your PC resources is that, when your laptop lid is closed, it will render to your screen
only using CPU resources (your GPU will be completely idle, a complete shame).

There are tons of posts that you can find on [DisplayLink (The makers of USB graphics drivers)](http://www.displaylink.com), and on some windows forums where
lots of users nag that their mouse is lagging or similar problems related to performance. The guys at DisplayLink and Windows are supposedly working together
to have better support for USB graphics on Windows, but I have tested combinations of DisplayLink drivers ranging from 7.8.x till 8.1.alpha, and all of those exhibit
performance problems. The only combination that worked for me was 7.9.x, without the "recent" windows updates.
So this configuration will break whenever you update either windows or DisplayLink, and is therefore not sustainable.
Furthermore, the 7.x DisplayLink drivers are no longer compatible with recent versions of Windows.

# The solution: Make your laptop lid think it is a hard disk volume

Yes, It is this weird, and this hacky!
I found parts of this solution somewhere deep inside some forums (that I can no longer find to give credit to).

The solution is as follows:

1. Open Device Manager.
2. Select your lid driver (somewhere under System devices category), and chose to "update driver software".
3. When asked from where the driver should be updated, make sure you chose from a list of drivers.
4. Search for `Volume Manager` driver, and confirm the changes.

This will make Windows avoid turning off your laptop monitor, even when the lid is closed (Because it now thinks it is a hard drive :smile:).
With that in place, rendering will still be done by your graphics card, and your CPU will no longer be devoured by the DisplayLink driver.

# Morals

This solution, as ugly as it may look or sound, actually works.
What I have learned from this is the following:

* Do not purchase a USB monitor, the tech is still not really mature. It is a waste of time & money.
* If you reallly need this setup (In my case, my laptop screen was burning my retina), make sure you buy a screen with VGA or HDMI input.
* Sometimes things can magically work the way you want to by using some black magic, try to avoid those situations :smile: