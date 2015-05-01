---
layout: post
title: "Too many authentication failures"
description: ""
category: ubuntu
tags: [ssh]
date: 2015-05-01 16:16:49
---
{% include JB/setup %}

I've been trying to login from my desktop PC to my Raspberry Pi. It worked before but recently I wasn't able to ssh from it. 

I tried `ssh -v pi@raspberry` and it seems that it has these errors repeated 5 times for different keys.

    debug1: Authentications that can continue: publickey,password
    Offering RSA public key: ansshkey@something

Turns out that my desktop has too many keys in `ssh-add -l` that it kept on trying to login with keys. `ssh-add -D` did not simply work. You have to manually remove unneeded keys from `~/.ssh/` folder.
Finally I can login again ^o^