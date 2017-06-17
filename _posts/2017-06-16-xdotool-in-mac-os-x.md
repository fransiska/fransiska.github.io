---
layout: post
title: xdotool in Mac OS X
description: ""
category: mac
tags: [mac,programming,compile]
date: 2017-06-16 00:00:00 +07:00
---

`xdotool` is a command line tool used to emulate mouse and keyboard. 
The version on macport is too old so it [doesn't compile](https://stackoverflow.com/questions/43413100/installing-xdotool-through-port-fails) on Mac OS Sierra (last update was 2011).

### xkbcommon
1. Clone [libxkbcommon](https://github.com/xkbcommon/libxkbcommon). This is required to compile `xdotool`.
```cpp
#include <xkbcommon/xkbcommon.h>
```
2. To use autogen.sh, it requires xorg-macros 1.16.
```bash
sudo port install xorg-util-macros
```
3. When I first try to run `make`, this error comes up.
```
YACC     src/xkbcomp/parser.c
/Users/fransiska/Git/libxkbcommon/src/xkbcomp/parser.y:220.5-9: syntax error, unexpected type, expecting string or identifier
```
  The cause is that `bison` version is too old. Mac comes with the version 2.3. So we need to [replace it](http://robupcraft.com/install-bison-mac/).
```bash
sudo port install bison
cd /usr/bin/
sudo mv bison bison-2.3
sudo ln -s /opt/local/bin/bison bison
```
4. Compile `libxkbcommon`.
```bash
./autogen.sh --enable-shared
make
```

### xdotool

1. Clone [xdotool](https://github.com/jordansissel/xdotool).
2. Fix `Makefile` to include the newly compiled `libxkbcommon`. 
```make
DEFAULT_LIBS=-L/usr/X11R6/lib -L/usr/local/lib -lX11 -lXtst -lXinerama -lxkbcommon -L/Users/fransiska/Git/libxkbcommon/.libs
DEFAULT_INC=-I/usr/X11R6/include -I/usr/local/include -I/Users/fransiska/Git/libxkbcommon
```
I cloned the repository into `/Users/fransiska/Git/libxkbcommon`.
3. Compile it.
```bash
make
sudo make install
```
4. Link also the library for `libxkbcommon` (`xdotool` asks it).
```bash
cd /usr/local/lib/
sudo ln -s /Users/fransiska/Git/libxkbcommon/.libs/libxkbcommon*dylib .
sudo ln -s /Users/fransiska/Git/libxkbcommon/.libs/libxkbcommon*a .
```
5. Now that it launches, when you try to send commands, this error shows up.
```
Error: XTEST extension unavailable on '(null)'.
```
You need to [enable it](https://stackoverflow.com/questions/1264210/does-mac-x11-have-the-xtest-extension).
```bash
defaults write org.x.X11 enable_test_extensions -boolean true
defaults write org.macosforge.xquartz.X11 enable_test_extensions -bool yes
```
6. Restart XQuarts. Unfortunately, this only works on X terminals, so you can only test it on the xterm.
One alternative to this for Mac OS is [cliclick](https://www.bluem.net/en/mac/cliclick/). 