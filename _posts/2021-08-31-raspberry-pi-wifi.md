---
layout: post
title: Disable Raspberry Pi's WiFi
tags: [raspberrypi]
---

Add this line into `/boot/config.txt` to disable Raspberry Pi's default Wireless LAN interface (eg. To always use an external dongle instead):

```
dtoverlay=disable-wifi
```
