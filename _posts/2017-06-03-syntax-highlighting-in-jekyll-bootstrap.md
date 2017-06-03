---
layout: post
title: Syntax highlighting in Jekyll Bootstrap
description: ""
category: jekyll
tags: [jekyll, programming]
date: 2017-06-03 19:24:00 +07:00
---

[This](https://benhur07b.github.io/2017/03/25/add-syntax-highlighting-to-your-jekyll-site-with-rouge.html) is a very detailed guide on how to add syntax highlighting in Jekyll (Github Pages).
Basically, `rouge` will slice the codes accordingly into separate HTML tags, the css will color it according to your theme. `kramdown` is the Markdown processor supported in Github Pages. What I did on my Jekyll Bootstrap:

1. Install `rouge` and `kramdown` to generate css and render locally in the same manner as Github Pages.
    ```shell
    gem install kramdown rouge
    ```
  
2. Update `_config.yml`
    ```yaml
    markdown: kramdown
    highlighter: rouge
    kramdown:
      input: GFM #Github Flavored Markdown
      hard_wrap: false  
      syntax_highlighter: rouge
    ```

3. Create css file to color the syntax. I use the Bootstrap-3 theme.
    ```shell
    rougify style monokai > assets/themes/bootstrap-3/css/syntax.css  
    ```

4. Add css link in `<head>` in `_includes/themes/bootstrap-3/default.html`. 
    ```html
    <link href="{{ ASSET_PATH }}/css/syntax.css" rel="stylesheet">  
    ```

Jekyll 3.3.1 did not render the indented code block for numbered lists correctly. When I did `bundle update` and was updated to jekyll 3.4.3, it showed up fine.