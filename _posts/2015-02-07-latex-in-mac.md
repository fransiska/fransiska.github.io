---
layout: post
title: "Latex in Mac"
description: ""
category: latex
tags:
- mac
- latex
date: 2015-02-07 03:13:09
---
{% include JB/setup %}

OSX 10.8.5, UpTeX installed, (Not sure what else I installed).

Running `tlmgr` installs package in `/usr/local/texlive/2013basic/texmf-dist/tex/latex/biblatex`.
Put a symbolic link into `/Applications/UpTeX.app/teTeX/share/texmf-dist/tex/latex` and run texhash.

    $texhash
    texhash: Updating /Applications/UpTeX.app/teTeX/share/texmf/ls-R...
    texhash: Updating /Applications/UpTeX.app/teTeX/share/texmf-config/ls-R...
    texhash: Updating /Applications/UpTeX.app/teTeX/share/texmf-dist/ls-R...
    texhash: Updating /Applications/UpTeX.app/teTeX/share/texmf-var/ls-R...
    texhash: Updating /Applications/UpTeX.app/texfonts/ls-R...
    texhash: Done.

Then I can run the new package with `pdflatex`.