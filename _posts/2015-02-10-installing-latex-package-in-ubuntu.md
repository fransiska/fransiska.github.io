---
layout: post
title: "installing latex package in ubuntu"
description: ""
category: latex,ubuntu
tags: [latex,ubuntu]
date: 2015-02-10 11:11:28
---
{% include JB/setup %}

Download zip file and copy it to the install folder, then do `texhash`

     sudo unzip ~/Downloads/glossaries.tds.zip -d /usr/local/share/texmf
     sudo texhash