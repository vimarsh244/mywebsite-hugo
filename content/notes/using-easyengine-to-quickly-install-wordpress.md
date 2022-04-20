+++
author = "Vimarsh"
categories = []
date = ""
description = "Easily install Wordpress on any small Virtual Machine (VM) from a cloud provider."
images = []
tags = []
title = "Using Easyengine to quickly install WordPress"
url = "/notes/using-easyengine-to-quickly-install-wordpress"

+++
It is much efficient and better to install WordPress on VMs from reputable cloud providers, which I do for a lot of websites.

Easyengine is an amazing tool to do so. Here is how I do it!

**Install EasyEngine on Linux**

    wget -qO ee rt.cx/ee4 && sudo bash ee

From <[https://easyengine.io/](https://easyengine.io/ "https://easyengine.io/")>

**Run this**

replace [website.com](vimarsh.info "Text in command") → your domain of choice

admin → WordPress admin user

Passw0Rd → A strong Password

It will also automatically provision auto-renewing SSL certificate for your website.

    sudo ee site create website.com --type=wp --admin-user=admin --admin-pass=Passw0Rd

    sudo ee site update website.com --ssl=le