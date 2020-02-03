---
layout: post
title: CORS and SOP and curl
category: web
tags: [web, security, cors, sop, curl]
---

By default, browser disallow website A (eg. http://localhost:5000) to access data (eg. call REST API) from website B (eg. http://localhost). This is called SOP (Same Origin Policy). If we want to allow this, website B needs to enable CORS (Cross-Origin Resource Sharing).

We can, however, use `<img>` tags with sources from another website by default, it is called embedding.

SOP is used so that when you're logged in to your bank account, which leaves a cookie, while at the same time opening a malicious website, this malicious website will not be able to send request to the bank. If there is no SOP, the malicious website can send request **through your browser pretending that it is you since your browser has your cookie**.

When you do `curl` to the bank website, it won't be blocked by SOP since it's directly between you and the bank website. 

Ref:
- [Stackoverflow brief explanation](https://stackoverflow.com/a/28762923)
- [More in depth explanation and code examples](https://web.dev/same-origin-policy/)

