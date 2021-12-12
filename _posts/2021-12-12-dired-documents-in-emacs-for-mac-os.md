---
layout: post
title: Dired Documents in Emacs for Mac OS
---

I don't usually open files from Documents folder in Emacs. But I was trying to open an Arduino files, which by default is created in Documents folder. And I found out I couldn't dired the Documents dir (Not sure if I was able to open the file). The error was:

```
Listing directory failed but ‘access-file’ worked
```

### Solution

It's caused by Mac OS Privacy settings.

1. `Settings` -> `General Settings` -> `Security & Privacy` -> `Privacy` -> `Full Disk Access`
2. Check Emacs (Require restart)
3. Click +, add `/usr/bin/ruby` (I added this after restarting Emacs, did not require other restart. This was the one that let me do the dired)

- [[ref](https://emacs.stackexchange.com/a/53037)]
