---
layout: post
title: Combine PDF on Mac OS X
description: ""
category: mac
tags: [mac,command line,pdf]
date: 2017-06-15 01:22:00 +07:00
---

I wanted to combine some PDFs, but apparently `pdftk` is not compilable on Mac OS Sierra.

```
Error: pdftk currently does not build on OS X 10.11 or greater.
Error: See https://trac.macports.org/ticket/48528
Error: Failed to fetch pdftk: incompatible OS X version
```

But [this trick](http://gotofritz.net/blog/howto/joining-pdf-files-in-os-x-from-the-command-line/) works.

```bash
/System/Library/Automator/Combine PDF Pages.action/Contents/Resources/join.py -o combined.pdf 1.pdf 2.pdf
```