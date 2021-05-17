---
title: Install Nextcloud
author: Vimarsh
date: 2021-05-16T23:00:00+05:30
url: "/blog/installing-nextcloud"
images:
- "/uploads/2021/05/17/optimized-dallas-reedy-f2htc_cf4jo-unsplash.jpg"
description: Nextcloud is one of the most popular apps to regain control of your digital
  life. The self-hosted productivity platform that keeps you in control
categories:
- Tutorial
- Tech
- Blog post a day
tags:
- Tutorial
- Docs
- Nextcloud
- Self Hosted

---
**What is Nextcloud?**

**Nextcloud** is a suite of [client-server software](https://en.wikipedia.org/wiki/Client%E2%80%93server_model "Client–server model") for creating and using [file hosting services](https://en.wikipedia.org/wiki/File_hosting_service "File hosting service"). It is enterprise-ready with comprehensive support options. Being [free and open-source](https://en.wikipedia.org/wiki/Free_and_open-source "Free and open-source") software, anyone is allowed to install and operate it on their own [private server](https://en.wikipedia.org/wiki/Private_server) devices.

Nextcloud is functionally similar to [Dropbox](https://en.wikipedia.org/wiki/Dropbox_(service) "Private server"), [Office 365](https://en.wikipedia.org/wiki/Office_365) or [Google Drive](https://en.wikipedia.org/wiki/Google_Drive "Google Drive") when used with its integrated office suite solutions [Collabora Online](https://en.wikipedia.org/wiki/Collabora_Online "Collabora Online") or [OnlyOffice](https://en.wikipedia.org/wiki/OnlyOffice "OnlyOffice"). It can be hosted in the cloud or on-premise. It is scalable from home office solutions based on the low cost Raspberry Pi all the way through to full sized data centre solutions that support millions of users. ([source](https://en.wikipedia.org/wiki/Nextcloud))

Basically you can have your own Google Photos, MS Office, Google Drive, Kindle and much more, all hosted on your own server.

### Installing Nextcloud

In my limited testing I have found Nextcloud instance to be the most stable with Ubuntu or ubuntu-based linux distro.

**Step 1**

Updating default packages

    sudo apt-get update && sudo apt-get upgrade -y

**Step 2**

Configure firewall rules using IPtables or UFW whichever is preferred.

I would seriously recommend using snap store for installation, as not only is it crossplatform it has high stability and updates automatically.

    sudo snap install nextcloud

**Configuring Users and Domain**

Make sure to configure the domain you want to use to point to the IP address of your machine and run the following.

    sudo nextcloud.manual-install user password
    
    sudo nextcloud.occ config:system:set trusted_domains 1 --value=example.com

**Removing nextcloud branding**

Although I personally do not recommend it, if you are using Nextcloud for business purposes it doesn't look promising to have a big branding. You an easily remove the watermark as doccumented:

Edit the config.php file located here: `/var/snap/nextcloud/21796/nextcloud/config`

Adding the following and restarting nextcloud service will fix it

    'simpleSignUpLink.shown' => false,

### List of some useful apps

As you might have guessed, you can install several first party and other third party apps too, in your nextcloud instance with just one click. Here are someof my favourite apps that I use on daly basis with Nextcloud.

* Only Office // a lightweight MS Office type expirience (also supports live collaboration)
* Community doccument server // no need for another server to facilitate Only Office
* Nextcloud talk // Chat app but you host it yourself
* Notes // simple minimalist note taking

### Conclusion

Nextcloud is really enjoyable and easy to use software. The learning curve is also pretty low if just getting into self hosting and reducing relliance on third party tech giants. Installing apps is super easy and it has an actively growing community with now even proper support for Raspberry Pis (a lot of new apps supporting this).

I have been pretty happy with my Nextcloud configuration. Also, its android app is amazing and the sync on Windows work flawlessly. File sharing is also available with multiple links for same folder (some features not even available on Google Drive, Onedrive, etc.) Use it everyday and the uptime has been crazy - 100% never had to even reboot for any update or anything ever since I got it up.

![Nextcloud Uptime](/uploads/2021/05/17/nextcloud-install.png)