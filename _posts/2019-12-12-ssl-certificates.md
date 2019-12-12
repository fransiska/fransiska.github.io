---
layout: post
title: Setting Up SSL Certificates in Apache
category: web
tags: [ssl,web,apache]
---

I have not fully understood this, I will just detail out what I did. I used AWS AMI (version 1) and Apache (httpd).
There are 2 things that I set up using SSL certificates:
1. HTTPS: Setting up Certificate for HTTPS connection. This is the one that can be seen by clicking the lock button at the address bar of the web browser.
2. Client certificate: Securing the connection by enforcing the use of a client certificate to connect to a server.

### HTTPS

You can either make a self-signed certificate, buy one, or get a free one from place such as [Let's Encrypt](https://letsencrypt.org/). I used the last option and since certificates expire after certain time, a lot of people uses [Certbot](https://certbot.eff.org/instructions) to do the automatic registration to Let's Encrypt (For AWS AMI, I referred to the instruction for Cent OS 6). What you need to make sure is the `Common Name` has to be the same as the URL it is going to launch at (what is set as the server name at the Apache config file).

#### DNS for subdomain

### Client certificate

#### Server CA
#### Client certificate
