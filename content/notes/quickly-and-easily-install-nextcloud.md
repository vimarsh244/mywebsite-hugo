+++
author = "Vimarsh"
categories = ["tutorial"]
date = ""
description = "Simple instructions to install NextCloud"
draft = true
images = []
tags = []
title = "Quickly and easily install Nextcloud"
url = "/notes/quickly-and-easily-install-nextcloud"

+++
## Install Nextcloud - My Way

Rule 1: use Ubuntu / any other debian OS

    sudo apt-get update && sudo apt-get upgrade -y

### Clear all firewall rules

I believe its better to configure firewall from the Cloud Provider's settings.

    sudo iptables -P INPUT ACCEPT
    sudo iptables -P OUTPUT ACCEPT
    sudo iptables -P FORWARD ACCEPT
    sudo iptables -F

You can also alternatively after clearing existing rules, install UFW and manage firewall rules from there.

## Installing Nextcloud

    sudo snap install nextcloud

From <[https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-nextcloud-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-nextcloud-on-ubuntu-18-04 "https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-nextcloud-on-ubuntu-18-04")>

Setting username and password for admin user followed by setting up trusted domains for accessing the settings.

    sudo nextcloud.manual-install user password

    sudo nextcloud.occ config:system:set trusted_domains 1 --value=www.vimarsh.info

### Remove get your own Nextcloud server branding from footer

goto:  _/var/snap/nextcloud/21796/nextcloud/config_

Edit file config.php

Add in the list this:

    'simpleSignUpLink.shown' =>

From <[https://help.nextcloud.com/t/remove-link-get-your-own-free-account/41131/5](https://help.nextcloud.com/t/remove-link-get-your-own-free-account/41131/5 "https://help.nextcloud.com/t/remove-link-get-your-own-free-account/41131/5")