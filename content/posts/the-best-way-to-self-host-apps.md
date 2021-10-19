+++
author = "Vimarsh"
categories = ["tech", "tutorial"]
date = 2021-10-16T18:30:00Z
description = ""
draft = true
images = ["/uploads/2021/10/19/raspberry-pi-1719219_960_720.jpg"]
tags = ["tech", "self hosting"]
title = "The Best way to self host apps"
url = "/blog/the-best-way-to-self-host"

+++
## What is Self-Hosting?

Self-hosting means the practice of running some services yourself and maintaining and controlling it to the fullest extent you can. There are several reasons to self-host apps - you might be paranoid about Google / Apple having your data (photos, email, etc.), you might want to access a remote PC for work / school or host some website for your family and friends or just have fun tinkering and trying out new apps.

You can host a Google Photos like app, your own email client, a Wordpress website, Repl.it type service and much more. Although there are well written tutorials regarding all those different apps, I have found managing many apps and quickly trying out or debugging to be a huge bottleneck. It was a hassle and not the most fun thing to do especially when you want it to always work. Until I had found [CapRover](https://www.google.com/url?q=https%3A%2F%2Fcaprover.com%2F&sa=D&sntz=1&usg=AFQjCNED-QL3qoKRG4yjooddkK6fCbUzSA).

## What is CapRover?

From its [website ](https://www.google.com/url?q=https%3A%2F%2Fcaprover.com%2F&sa=D&sntz=1&usg=AFQjCNED-QL3qoKRG4yjooddkK6fCbUzSA)-

> CapRover is an extremely easy to use app/database deployment & web server manager for your NodeJS, Python, PHP, ASP.NET, Ruby, MySQL, MongoDB, Postgres, WordPress (and etc...) applications!

CapRover basically is a simple tool to manage, create and deploy all types of applications. It uses Docker at its core and has a powerful and super functional & beautiful GUI to manage everything. It has an amazing collection of [one-click to install apps](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fcaprover%2Fone-click-apps&sa=D&sntz=1&usg=AFQjCNGS4OtabN-JJGSKEob6AYtmonl7vw) and it auto generates and renews Let's Encrypt SSL certificates, making it as easy as clicking a button to deploy your own Google Drive alternative. The best part is that even after removing the CapRover utility, all the apps continue to function. Did I mention it's open-source!

([GitHub](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fcaprover%2Fcaprover&sa=D&sntz=1&usg=AFQjCNEdYYiTjYP4FeLNux1sJ7Fd5WsvgQ))

## Getting Started

First off, you need a system to install CapRover on. For self-hosting the best thing is to have a server / old-pc / raspberry pi running in your home. You can also use a reputed Cloud Provider like [Digital Ocean](https://www.google.com/url?q=https%3A%2F%2Fm.do.co%2Fc%2F32b907edbd54&sa=D&sntz=1&usg=AFQjCNF8xd0czaPso6rnbX1_61XvWMvZkw) (affiliate link) to quickly create a small VM for free and play with it.

Currently, [Oracle Cloud](https://www.google.com/url?q=https%3A%2F%2Fwww.oracle.com%2Fcloud%2Ffree%2F&sa=D&sntz=1&usg=AFQjCNF4hxj3VpiRQAFE7M30kMla2wjFRg) is offering amazing Always-Free tier with 2 AMD CPU cores or 4 ARM cores and 24 Gigs of RAM, also 200 GB storage, which is more than enough for most use-cases.

You can follow an [amazing guide on their website](https://www.google.com/url?q=https%3A%2F%2Fcaprover.com%2Fdocs%2Fget-started.html&sa=D&sntz=1&usg=AFQjCNFIjt3yibot8IVCIagpSJcAl-USKg) to quickly get started, or **expand the Steps** below.

## Steps

I would recommend Ubuntu as the distro of choice because most docker images function best with it. Official recomendation is for Ubuntu 18.04 but for me 20.04 has worked fine.

Step 0 : SSH into the machine (VM or bare-metal and follow these instructions)

**Code to Upgrade packages:**

    sudo apt-get update && sudo apt-get upgrade -y

To [Install Docker](https://www.google.com/url?q=https%3A%2F%2Fdocs.docker.com%2Fengine%2Finstall%2Fubuntu%2F%23installation-methods&sa=D&sntz=1&usg=AFQjCNGBJDexvFJyTWxjKJb2qqUvFuqd2A)

    sudo apt-get install \
    	apt-transport-https \
    	ca-certificates \
    	curl \
    	gnupg \
    	lsb-release

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

    echo \"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    sudo apt-get update
    
    sudo apt-get install docker-ce docker-ce-cli containerd.io

To **verify if Docker is working**:

    sudo docker run hello-world

**Configure Firewall**

Clear all already set iptables if set by your cloud provider and configure firewall via UFW (personal preference)

Also make sure to allow ports which you are _actively using for caprover_ from your router or cloud provider's console.

    sudo ufw allow 22,80,443,3000,996,7946,4789,2377/tcp; sudo ufw allow 7946,4789,2377/udp;
    
    sudo ufw enable

### Installing Caprover

Just run the following line, sit back and enjoy!

    sudo docker run -p 80:80 -p 443:443 -p 3000:3000 -v /var/run/docker.sock:/var/run/docker.sock -v /captain:/captain caprover/caprover

NOTE: **Do not** change the port mappings. CapRover only works on the specified ports.

**Configure domain name** (after port forwarding if hosting in your home)

\*.domain.name should point to publicly reachable IP address of the machine

Assuming you have npm installed on **your local machine** (e.g., your laptop), simply run (add sudo if needed):

    npm install -g caprover

Then, run

    caprover serversetup

and follow the instructions shown.

CapRover should be available on the domain name you configured it with.

Once you login you will see a simple UI, click on one-click apps.

![CapRover Dashboard Screenshot](/uploads/2021/10/19/screenshot-2021-10-17-164023.png)

## Some Useful and Amazing Apps

Firstly, these are some apps which I use and love, though your preference may vary. Secondly, it's not just that you can JUST install the apps already there, but in fact you can install any you like ([instructions for same](https://www.google.com/url?q=https%3A%2F%2Fcaprover.com%2Fdocs%2Fdeployment-methods.html&sa=D&sntz=1&usg=AFQjCNGGO22rn1BgVghmxEeOfxTIB2u6lg)), although most well maintained apps are already available as one-click images.

If you are using an ARM processor (Raspberry Pi / Graviton instance, etc.) some images might not work and some tweaks may be needed in the _captain-definition_ file. One such example for WordPress is attached below, and I will be adding others as and when I find compatibility issues.

**Nextcloud**

It is a must have all-in-one platform. It is Google Drive + Photos + Docs + iMessage combined. In fact it also has a huge library of apps you can install, within a Nextcloud instance. [Link](https://www.google.com/url?q=https%3A%2F%2Fnextcloud.com%2F&sa=D&sntz=1&usg=AFQjCNGwO5XFVqs7RdPinsOEqTFOSpcKrg)

**Duplicati**

Duplicati is a backup solution that takes encrypted backups to almost any provider of your choice (Backblaze, OneDrive, etc.) You might want to backup Nextcloud photos / notes or any other file to an offsite location. [Link](https://www.google.com/url?q=https%3A%2F%2Fwww.duplicati.com%2F&sa=D&sntz=1&usg=AFQjCNEmySL7Wc9PKKsuh6SxhDD5nkG8HQ)

**Invidious**

An alternative front-end for YouTube. Very customizable and mobile-friendly! [Link](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fiv-org%2Finvidious&sa=D&sntz=1&usg=AFQjCNFbtZIFOTe5kb_uMLh-zmlLm0hANg)

**Plausible Analytics**

Privacy friendly analytics platform for your websites. [Link](https://www.google.com/url?q=https%3A%2F%2Fplausible.io%2Fself-hosted-web-analytics&sa=D&sntz=1&usg=AFQjCNFywiMENiLazFWbPiRh9nL8pE90vg)

**Poste.io**

A complete email server. Email hosting is hard, but with Poste.io not so much. Super easy and quick to setup. [Link](https://www.google.com/url?q=https%3A%2F%2Fposte.io%2F&sa=D&sntz=1&usg=AFQjCNFOzOM-VHhUKSQLXL3H904zYJZhHA)

**Searx**

A privacy-respecting meta search engine. Proxy your Google search results. Use multiple search engines - all from one place. [Link](https://www.google.com/url?q=https%3A%2F%2Fsearx.me%2F&sa=D&sntz=1&usg=AFQjCNH0OpuoP8HI1gBoZ3PIZD2NK-bpWg)

**PrivateBin**

PrivateBin is a minimalist, open source online pastebin where the server has zero knowledge of pasted data. [Link](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2FPrivateBin%2FPrivateBin&sa=D&sntz=1&usg=AFQjCNErWw9d4NCksf74yRsNCCJYC37IBg)

**VScode via code-server**

Run VS Code on any machine anywhere and access it in the browser. This has been a game-changer for me personally as now I can code my school projects and assignments from a chromebook, desktop PC, or any other device, with continuity and is maintained perfectly between all the devices. [Link](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fcdr%2Fcode-server&sa=D&sntz=1&usg=AFQjCNG4gb4oLQNhEuGy0EnVUp1Dh57Crw)

**Others**

There are multiple RSS feed readers, database images, website platforms (Ghost, WP, etc.), File managers, Joplin server, [Adguard Home](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2FAdguardTeam%2FAdguardHome&sa=D&sntz=1&usg=AFQjCNEwIdZWVxnX9h-H136_Rb7l2BXWzA), [Plex](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fplexinc&sa=D&sntz=1&usg=AFQjCNGUXM9mA7_zTfoqJnwCMScXL5V3Yg), [Etherpad](https://www.google.com/url?q=https%3A%2F%2Fetherpad.org%2F&sa=D&sntz=1&usg=AFQjCNEblm2NOUjagaPEUbmXS6v4awIy0w), [Gitea](https://www.google.com/url?q=https%3A%2F%2Fgitea.io%2F&sa=D&sntz=1&usg=AFQjCNGLvHe85GC6PmVsaQReN2lEY8Y_Iw) and many more. With CapRover you can easily try out as many as you want. Also you can host custom docker images, apps, etc.

## Conclusion

With ability to easily (with press of a button) install and try out apps, auto generate SSL certs, and an amazing monitoring utility [NetData](https://www.google.com/url?q=https%3A%2F%2Fcaprover.com%2Fdocs%2Fresource-monitoring.html&sa=D&sntz=1&usg=AFQjCNECP4HdqnOkk014ZS9Bc5eDaEwQOQ) already bundled in, it is the best platform to self-host _most_ services (that offer docker images! - or which you can maintain). And probably the best for most users.

The only downside is that being a nodeJS application, its ram usage is a little high - although not even close to being a hinderance for most people.

***

Wordpress ARM CapRover Template