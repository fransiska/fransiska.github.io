---
layout: post
title: Dashboard for ledger
category: ledger
tags: [programming,ledger]
---

I've been using org-mode to manually make various reports for ledger. Few years ago I [ledger-web](https://github.com/peterkeen/ledger-web) to display the reports in browser from local machine, but I think I couldn't quite customize it at that time.

I was looking for something done using `flask` since I work with it a lot recently so I'm familiar with it. Also, something that directly uses `ledger` command would be better instead of saving the data to another format/database. I found [ledger-dashboard](https://github.com/Ikke/ledger-dashboard) and I find it easy to customize. I added months view and changed some of the dashboard view.

Next step, I want to add graphs! And maybe a more customizable board elements with simple settings like `register`/`balance`, title of the element, and the pattern.