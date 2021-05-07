---
layout: post
title: Comparing binary files
category: emacs
tags: [emacs]
---

Comparing bytes differences between 2 binary files.

1. Open a binary file
2. M-x hexl-mode
3. In another buffer, open another binary file
4. M-x hexl-mode
5. M-x ediff-buffers
6. Press enter twice to automatically compare the last two buffers
7. In the small ediff popup window, press `n` to go to the next difference
8. Press `*` to show more detailed difference by byte
