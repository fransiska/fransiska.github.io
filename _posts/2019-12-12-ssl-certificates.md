---
layout: post
title: Setting Up SSL Certificates in Apache (Part 1)
category: web
tags: [ssl,web,apache]
---

I have not fully understood this, I will just detail out what I did. I used AWS AMI (version 1) and Apache (httpd).
There are 2 things that I set up using SSL certificates:
1. **HTTPS**: Setting up Certificate for HTTPS connection. This certificate used for encryption that can be confirmed by clicking the lock button at the address bar of the web browser. By having https, data transfers between server and client are encrypted. The certificate
2. **Client certificate**: Securing the connection by enforcing the use of a client certificate to connect to a server.

### Setting up a web server in AWS

I used AWS EC2, which is a Linux machine where you can ssh into. The OS image that I used was AWS AMI (version 1). Just like a normal Linux machine, we can set up a web server using Apache, which I won't detail out here.

### HTTPS

You can either make a self-signed certificate, buy one, or get a free one from place such as [Let's Encrypt](https://letsencrypt.org/). I used the last option and since certificates expire after certain time, a lot of people uses [Certbot](https://certbot.eff.org/instructions) to do the automatic registration to Let's Encrypt.

Steps:
1. Set up Apache config to serve the web at port 80. Edit the file `/etc/httpd/conf.d/my-server.conf`. This settings used Apache version

    ```
    <VirtualHost *:80>
        ServerName example.com

        DocumentRoot /var/www/public

        DirectoryIndex index.php index.html

        <Directory /var/www/public/>
            Options FollowSymLinks
            AllowOverride All

            Require all granted
        </Directory>

        ErrorLog /var/log/httpd/my-server-error.log

        LogLevel warn

        SSLCertificateFile /etc/letsencrypt/live/example.com/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
        Include /etc/letsencrypt/options-ssl-apache.conf
    </VirtualHost>
    ```

     Rename other conf such as `ssl.conf` and `userdir.conf` to an extension other than `.conf` so that it doesn't conflict with our config.

2. Run Certbot. (For AWS AMI, I referred to the instruction for Cent OS 6)What you need to make sure is the `Common Name` has to be the same as the URL it is going to launch at (what is set as the server name at the Apache config file).

3. Set up Apache config to serve the web at port 443 and redirect port 80 to port 443
    ```
    Listen 443
    <VirtualHost *:443>
        ServerName example.com
        DocumentRoot /var/www/public

        SSLEngine on

        SSLCACertificateFile /etc/pki/CA-example/ca.pem
        SSLVerifyClient require
        SSLVerifyDepth 1

        DirectoryIndex index.php index.html

        <Directory /var/www/public/>
            SSLRequire %{SSL_CLIENT_S_DN_CN} in {"example.com"}

            Options FollowSymLinks
            AllowOverride All

            Require all granted
        </Directory>

        ErrorLog /var/log/httpd/my-server-error.log

        LogLevel warn

        SSLCertificateFile /etc/letsencrypt/live/example.com/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
        Include /etc/letsencrypt/options-ssl-apache.conf
    </VirtualHost>

    <VirtualHost *:80>
      RewriteEngine on
      RewriteCond %{HTTPS} off
      RewriteRule ^/(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
    </VirtualHost>
    ```

### To write in the next part

- [ ] DNS for subdomain
- [ ] Client certificate
    - [ ] Server CA
    - [ ] Client certificate
