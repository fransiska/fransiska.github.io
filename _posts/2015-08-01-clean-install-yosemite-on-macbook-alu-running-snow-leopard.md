---
layout: post
title: "Clean install Yosemite on Macbook Alu running Snow Leopard"
description: ""
category: mac
tags: [mac, install]
date: 2015-08-01 22:22:18
---
{% include JB/setup %}

## Step 1
Make an installer drive on a USB stick or a USB harddrive. Use a GUID partition, Extended Mac OS X Journaling. Download Yosemite installer on App Store. 

`createinstallmedia` does not work on Snow Leopards.

Instead, use *Option 2* of [this article](http://www.macworld.com/article/2367748/how-to-make-a-bootable-os-x-10-10-yosemite-install-drive.html). I forgot the copying the .dmg at the top level of the drive and I got an [instalation error](http://www.insanelymac.com/forum/topic/301563-os-x-could-not-be-installed-on-your-computer/).

## Step 2
Back up current OS with [Carbon Copy Cloner](https://bombich.com) version 3 (I used 30-day-trial and it worked fine). My mac kept on crashing and it was because it was indexing the new harddrive while it was cloning. Make sure to *turn off indexing* on the Spotlight settings.

## Step 3
Erase current OS disk. Boot to the newly created boot drive by pressing `Option` key while the computer is starting up. Go to utilities and erase the old OS to an empty Mac OS Extended Journaling.

