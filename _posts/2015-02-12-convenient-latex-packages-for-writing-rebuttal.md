---
layout: post
title: "Convenient latex packages for writing rebuttal"
description: ""
category: latex
tags: [latex]
date: 2015-02-12 22:45:56
---
{% include JB/setup %}

catchfilebetweentags
--------------------
To quote from other tex file (ie. indicating that you have added this specific file in the paper).
In the file you want to quote:

    %<*tag>
    This is the line I want to quote.
    %</tag>

In rebuttal file:
   
    ...
    \usepackage{catchfilebetweentags}
    ...
    \ExecuteMetaData[path/to/file.ext]{tag}
    ...

xr
--
To get reference numbers from other file (ie. putting the same section/figure/table number in your rebuttal file as in your paper).

    ...
    \usepackage{xr}
    \externaldocument{path/to/file.ext}
    ...
    Section \ref{sec:Method}
    ...

xr-hyper
--------
Alternative of `xr`.
To get name of section of other file from reference name (ie. replaces `\nameref{sec:intro}` to Introduction). When you click the link, it links to the section of the linked pdf file! Neat!

In file to get reference from:

    ...
    \usepackage{xr-hyper} %put link between files
    \usepackage{hyperref} %for nameref, use [draft]{hyperref} for disabling linking
    ...
    \section{Introduction}\label{sec:intro}.
    ...

In rebuttal file:

    ...
    \usepackage{xr-hyper} %put link between files
    \usepackage{hyperref} %for nameref, use [draft]{hyperref} for disabling linking
    \externaldocument{path/to/ref/file.ext}
    ...
    As explained in Section \nameref{sec:intro}.
    ...

Remove the aux files of both, then compile (ie. run `pdflatex`) the original file **twice**, **then** compile the rebuttal file twice.

Same cite reference number
--------------------------
To get the same reference number as used in the original file.
You must compile the original file first and produce the `.bbl` file before compiling the rebuttal file.
This snippet below allow the **Reference** section to be hidden.

    \clearpage
    \newsavebox\mytempbib
    \savebox\mytempbib{\parbox{\textwidth}{\input{path/to/file.bbl}}}

latexdiff
---------
To see how different your initial submission is to your revision. I like to have my added words written in red and the deleted ones not shown (by default it is blue).
After doing `latexdiff draft.tex revision.tex > diff.tex`, edit `diff.tex`

    \providecommand{\DIFaddtex}[1]{ {\protect\color{red}#1} } %change this to red color
    \providecommand{\DIFdel}[1]{} % Don't show deleted text

Then compile `diff.tex` to produce the pdf.

Supplementary materials
-----------------------
To add "S" in front of table and figure numbers, insert at the header.

    \makeatletter 
    \setcounter{figure}{0}
    \renewcommand{\thefigure}{S\@arabic\c@figure}
    \setcounter{table}{0}
    \renewcommand{\thetable}{S\@arabic\c@table}
    \makeatother
