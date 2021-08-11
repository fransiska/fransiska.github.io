---
layout: post
title: Markdown to PDF
---

MacBook Pro 2016, macOS Catalina, version 10.5.7

### Install

- Install packages
    ```bash
    brew install basictex
    sudo tlmgr update --self --all
    
    # Not sure if these 3 are needed
    sudo tlmgr paper a4
    sudo tlmgr install collection-langjapanese
    sudo tlmgr install xecjk
    
    # Fix `! LaTeX Error: File `ctexhook.sty' not found.`
    sudo tlmgr install ctex
    ```
- To fix `! Package fontspec Error: The font "IPAexGothic" cannot be found.`, download fonts from [here](https://moji.or.jp/ipafont/ipaex00401/), unzip, and double click the `.ttf` file to open a window, click `Install font`
- There must be a simpler way to install... :confused: It's never easy to setup latex, especially for writing Japanese/Chinese/Korean

### Compile

I use a makefile so that the files can be ordered as I like. Note that Makefile indentation usually requires `TAB`.

```make
files = \
	index.md\
	$(wildcard files*.md)

output/manual.pdf: $(files)
	pandoc --pdf-engine=xelatex -V CJKmainfont=IPAexGothic
	  -V colorlinks=true \
	  --output=$@ $(files)
```

In terminal, type `make`
