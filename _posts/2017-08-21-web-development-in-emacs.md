---
layout: post
title: Web development in Emacs
category: emacs
tags: [programming,web,emacs]
---
<div id="table-of-contents">
  <h2>Table of Contents</h2>
  <div id="text-table-of-contents">
    <ol>
      <li><a href="#org3034412">Installed packages</a></li>
      <li><a href="#org3ea5d88">Automatically load <code>web-mode</code> when opening web-related files</a></li>
      <li><a href="#org0919792">Set indentations</a></li>
      <li><a href="#org0f9f7e0">Highlight of columns</a></li>
      <li><a href="#org9198251"><code>Company</code> settings</a></li>
      <li><a href="#orgcf2a3a8"><code>Emmet</code> settings</a></li>
    </ol>
  </div>
</div>

I've been writing a lot of html and css lately. I already used `web-mode` which provides highlighting and indentation for html, css, and javascript files in Emacs.
Recently I come accross [Emmet](<https://emmet.io>). It's not officially supported in Emacs, (well, most web developers use Sublime, I guess) but there is a package for <code>Emmet</code> in Emacs.
Here's the detail of my current web development settings in Emacs.


<a id="org3034412"></a>

### Installed packages

-   **web-mode**: highlighting, indentation, closing tags, jumping tags, commenting
-   **company-web**: completion of keywords as you type
-   **yasnippet**: shortcut to write a snippet
-   **emmet-mode**: smarter yasnippet


<a id="org3ea5d88"></a>

### Automatically load `web-mode` when opening web-related files

```emacs-lisp
(add-to-list 'auto-mode-alist '("\\.ts\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.html?\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.css?\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.js\\'" . web-mode))
```
{% include image name="emacs-mode-line.png" caption="When opening an html file, it will show Web on the emacs mode line." %}

<a id="org0919792"></a>

### Set indentations

`Hook` is executed when the mode is turned on. Here I set the indentations (I prefer indentation size of 2 spaces).

```emacs-lisp
(defun my-web-mode-hook ()
  "Hooks for Web mode."
  (setq web-mode-markup-indent-offset 2)
  (setq web-mode-code-indent-offset 2)
  (setq web-mode-css-indent-offset 2)
)
(add-hook 'web-mode-hook  'my-web-mode-hook)    
(setq tab-width 2)
```

<a id="org0f9f7e0"></a>

### Highlight of columns

I think this is neat!

```emacs-lisp
(setq web-mode-enable-current-column-highlight t)
(setq web-mode-enable-current-element-highlight t)
```

{% include image name="column-highlight.gif" %}

<a id="org9198251"></a>

### Company settings

Set the `company` completion vocabulary to css and html when in `web-mode`. This is combined into the indentations setting above.

```emacs-lisp
(defun my-web-mode-hook ()
  (set (make-local-variable 'company-backends) '(company-css company-web-html company-yasnippet company-files))
)
```

{% include image name="company-completion.gif" caption="The completion will show after some delay" %}

<a id="orgcf2a3a8"></a>

### <code>Emmet</code> settings

Turn on <code>Emmet</code> in `web-mode`.

    (add-hook 'web-mode-hook  'emmet-mode) 

`Web-mode` is able to switch modes into css (style tags) or js (script tags) in an html file. For <code>Emmet</code> to switch between html and css properly in the same document, this hook is added.

```emacs-lisp
(add-hook 'web-mode-before-auto-complete-hooks
    '(lambda ()
     (let ((web-mode-cur-language
  	    (web-mode-language-at-pos)))
               (if (string= web-mode-cur-language "php")
    	   (yas-activate-extra-mode 'php-mode)
      	 (yas-deactivate-extra-mode 'php-mode))
               (if (string= web-mode-cur-language "css")
    	   (setq emmet-use-css-transform t)
      	 (setq emmet-use-css-transform nil)))))
```

{% include image name="emmet.gif" caption="Emmet expands the bgc as background-color in style, and as a tag in html." %}

