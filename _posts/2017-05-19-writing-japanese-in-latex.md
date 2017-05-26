---
layout: post
title: "Writing Japanese in Latex"
description: ""
category: latex
tags: [latex]
date: 2017-05-19 01:27:19
---
{% include JB/setup %}

### Japanese
- compile with xelatex
- `\usepackage{xeCJK}`
- default fonts need to be set for macOS. I used `\setCJKmainfont{Hiragino Mincho Pro W3}` for the serif font

### Extra Latex packages with MacPort
Installing Latex with MacPorts wastes harddisk space, since I'd have to download single `.sty`s in bulk packages. I have yet to try installing MacTeX in this Mac, so [bulky MacPorts](https://trac.macports.org/wiki/TeXLivePackages) for now.