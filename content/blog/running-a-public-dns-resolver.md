---
title: Running a public DNS Resolver
author: Vimarsh
date: 2022-05-10
url: "/blog/running-a-public-dns-resolver"
images:
- "/from-temperory-writefreely-blog/Internet%20Encryption%20-%20decor%20image.jpg"
description: Here's how - I am running an Ad-blocking public DNS resolver with support for Encrypted DNS Requests using AdGuard Home.
categories:
- Tech
- Tutorial
tags:
- DNS
- server
- tech
---
### Accessing my Server

You can access my Ad blocking DNS server via these methods:
- Unsecured DNS (over port 53): `20.212.62.65`
- DNS over HTTPS (in Chrome, Firefox, etc.): `https://q.vimarsh.info/dns-query`
- DNS over TLS (mostly for Smartphones — you just add it in secure DNS setting): `q.vimarsh.info`

![Decor Image depicting Encryption inside 'Internet Pipeline'](/from-temperory-writefreely-blog/Internet%20Encryption%20-%20decor%20image.jpg)

### How-to

We will be using [AdGuard home](https://github.com/AdguardTeam/AdGuardHome). It is a little overkill for just resolving DNS but.. It is super simple to set up, can block advertisements at DNS level with simple blocklists, and can easily allow configuring Encrypted DNS (which would be extremely difficult with many other solutions).


p.s. This is what I did, and is probably not the safest thing to do…

Login to whatever distro's VM you choose (preferably Debian, Ubuntu)

```
sudo su

curl -s -S -L https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh -s -- -v
```
After it installs, go to port 3000 and setup admin credentials. Also, setup *.your.domain.name and your.domain.domain (the one you want to use for DNS) point to the public IP address of the VM.

While configuring you *might* see a warning (when doing 'All Interfaces') that says `bind: address already in use`, see the solution [here](https://github.com/AdguardTeam/AdGuardHome/wiki/FAQ#bindinuse).

Then install [certbot](https://certbot.eff.org/): If using Ubuntu as your distro, it's just `snap install --classic certbot`

Then to issue SSL certificates for your DNS domain and its subdomain run
```
sudo certbot certonly --preferred-challenges=dns --preferred-chain="ISRG Root X1" --manual
```
After you enter all details, it will show the path where the certificate is stored. Enter the path for the certificate and private key on the web UI Settings > Encryption Settings and enable encryption, and you are good to go!

### etc

I am using Microsoft Azure to host the DNS server… currently have student credits, and it should last for a year or so (hopefully). I do not guarantee the DNS server to always be up, and it could very well go down any time. Also, if you use the server, I can “in theory” track all the domains you query. Hopefully, Azure credits last through as there is no way I can find how much will it cost by end of month based on bandwidth usage, etc.
