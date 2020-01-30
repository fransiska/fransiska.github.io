---
layout: post
title: Firebase vs AWS EC2
category: web
tags: [web, web app, aws, ec2, firebase]
---

It's difficult to decide on which system is of a better use for a particular case, nevertheless, just a simple note of comparison of using Firebase (Hosting as well as Realtime Database) vs the traditional web server served in AWS EC2.

#### Firebase

- **Pro**: Fast to host a proof of concept or MVP, user authentication function is also already integrated, easy to setup
- **Con**: Hard to migrate to other system, you're basically stuck with Firebase

#### EC2

- **Pro**: Easy to manage and scale
- **Con**: Takes time to set up

Apparently, Python Flask is also usable for production (eg. [Pinterest](https://www.quora.com/What-challenges-has-Pinterest-encountered-with-Flask/answer/Steve-Cohen)).

To read: [NGINX](https://qr.ae/TD3jhV)
