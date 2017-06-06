---
layout: post
title: TeX in HTML
description: ""
category: jekyll
tags: [jekyll, latex]
date: 2017-06-06 20:10:00 +07:00
---

It is really easy to add TeX in HTML. I use [MathJax](http://docs.mathjax.org/en/latest/start.html).

1. Define the string that indicate the TeX block. Add this in the `<head>`. This is not needed in Jekyll, since the [kramdown](https://kramdown.gettalong.org/syntax.html#math-blocks) Markdown parser handles it.
   ````html
    <script type="text/x-mathjax-config">
      MathJax.Hub.Config({
      tex2jax: {inlineMath: [ ['$','$'], ['\\(','\\)'] ]}
      });
    </script>
   ````
   
2. Add in `<head>` the `.js` that converts these blocks. I add this in `_includes/themes/bootstrap-3/default.html` in my [Jekyll Bootstrap](http://jekyllbootstrap.com) installation (with Bootstrap 3 theme used).
   ```html
   <script type="text/javascript" async
      src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML">
   </script>
   ```

3. Add your TeX block in your `.html` or `.md`.
   ```
   $$a_1$$ \\(a_2\\)
   ```
   Will show as $$a_1$$ \\(a_2\\).

