---
layout: post
title: "Dual Boot Ubuntu 14.04.2 and Yosemite on Macbook Alu"
description: ""
category: mac
tags: [mac,ubuntu]
date: 2015-08-03 09:55:50
---
{% include JB/setup %}

It didn't work for me the first time (was stuck at the preparing for install screen), so I guess the order of the rEFInd and partition are important. [Reference](http://www.howtogeek.com/187410/how-to-install-and-dual-boot-linux-on-a-mac/).

I use a Macbook Alu (late 2008) with clean fresh install of Yosemite. 

## Step 1
Download Ubuntu for Mac. I used [ubuntu-14.04.2-desktop-amd64+mac.iso](http://cdimage.ubuntu.com/releases/14.04/release/).

Make boot drive of Ubuntu. The instructions using `dd` command didn't work for me. Probably because I use a partitioned harddrive instead of a USB stick? Anyways, I ended up burning the iso file instead. The instructions from [Ubuntu](https://help.ubuntu.com/community/BurningIsoHowto) works well.

## Step 2
Install `rEFInd`. Basically download the file (I used refind-bin-0.8.7) and run the install.sh script.
Shut down the computer and power on again, you should see the different boot screen.

## Step 3
Make the partition of the OS X smaller to make space for Ubuntu with Disk Utility. Do not make a new partition (I did it the first time, may be this was the problem). 

## Step 4
Restart and boot to the Ubuntu DVD. Choose *Install Ubuntu alongside Mac OS X*. And I had no problem booting into Ubuntu, except... my Wi-Fi is not working.

