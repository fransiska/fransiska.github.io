---
layout: post
title: "GUI with Touch Interface"
description: ""
category: programming
tags: [gtkmm, gtk, ubuntu, opengl, touch]
date: 2014-10-13 03:48:11
---
{% include JB/setup %}

I have the need to use a touch screen with a GUI running in Ubuntu.
Apparently, touch gestures has been developed since 2008!

###Setup 
The touch screen I use is a monitor by DELL, P2714T. This monitor uses *Advanced Silicon*, which was [supported](http://lii-enac.fr/en/architecture/linux-input/multitouch-devices.html) since Linux kernel 3.6.
The Ubuntu I use is 14.04 Trusty Tahr. The monitor works with the default setting. Chrome seems to crash the touch interface, but Chromium works nicely.

###Problem
Now, I have this GUI which was developed with *gtkmm2.4* and uses *gtkglarea* to display 3D model in OpenGL.
Touch events are only supported in GTK3. While I could possibly redevelop my GUI in GTK3, gtkglarea is not supported in Gtk3.
One of the solution is to use GLX to display the OpenGL. Gtk3 and GLX work nicely. 

, and touch gestures are only in GTK3.14
Trusty Tahr)