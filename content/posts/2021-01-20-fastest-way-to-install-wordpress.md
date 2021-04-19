---
title: Fastest way to install WordPress
author: Vimarsh
date: 2021-01-20T15:10:00.000+00:00
url: "/blog/fastest-way-to-install-wordpress/"
images:
- "/wp-content/uploads/2021/02/1_1hLHDT7VkTYf0vWKdQhvcHA.png"
categories:
- Tutorial
- Tech

---
I will be showing you the fastest way to install a fully functional WordPress website with an auto-renewing free SSL certificate in less than 3 commands. Let’s get started.

### Prerequisites

Make sure you are using Linux or Mac for installing WordPress. If you are deploying a website you might be using a virtual machine in the cloud for the same. _Stay tuned for another post on how you can get 2 free VMs forever on Oracle Cloud_

We will be using an open-source tool called [Easyengine](https://github.com/EasyEngine/easyengine) for installing and managing WordPress

![](https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd2afa4f.jpg)

> EasyEngine makes it greatly easy to manage Nginx, fast web-server software that consumes little memory when handling increasing volumes of concurrent users.

### Let’s get started

![](https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd33e0d4.jpg)

### SSH into the VM

You can use Putty / Powershell or Terminal to SSH into the VM

Also, make sure to update installed packages by running sudo apt-get update && sudo apt-get upgrade -y

### Install EasyEngine

Run the command

    # Install EasyEngine on Linux
    wget -qO ee rt.cx/ee4 && sudo bash ee
    
    # If installing EasyEngine on Mac for Local Development 
    brew install easyengine

### To install WordPress website run the command

`sudo ee site create website.com`

You can change the username & password of the WordPress install for security when you first open the website.

**Make sure to change** [**website.com**](http://website.com) **with your domain name**

I also recommend setting up Redis cache for a better performant website
`ee site create example.com –type=wp –mu=subdir –cache`.
Easyengine automatically creates the database, sets up secure username and passwords as well. Making the whole process super easy.

> Currently Easyengine does not support running without root privileges.

You can check out further options [here](https://github.com/EasyEngine/site-type-wp)

### Pointing the domain name to the server

Make sure you point your domain name to the server’s IP Address

Go to nameserver provider and set A record for your server.<figure class="wp-block-image">

![](https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd38c086.jpg) </figure>

**DNS Propogation might take time**

### Registering a SSL certificate

To get auto-renewing _free_ SSL certificate run

    sudo ee site update website.com

This will install an SSL certificate from [Let’s Encrypt](https://letsencrypt.org/) and change necessary database entries for HTTPS. The certificate also auto-renews 1 month before the expiry

_This might not work properly with Cloudflare_

**And that is all.** You have a fully functional WordPress website with auto-renewing SSL certificate. You can go to the WordPress admin panel [example.com/wp-admin](http://example.com/wp-admin) and start customizing.

_And you can also create more websites on the same instance_

### Some other Useful Commands<figure class="wp-block-image">

![](https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd3ebd94.jpg) </figure>

> Make sure to run with root privileges. You can use `sudo su` to run all following commands as root

### Installing PhPMyAdmin

Easyengine gives the option to enable PhPMyAdmin and other admin [tools](https://easyengine.io/handbook/admin-tools/#list-of-admin-tools)

To use that run 

    ee admin-tools enable example.com

By default, http authentication will be enabled. To view the username & password run ee auth list global

Then you can go to [example.com/ee-admin](http://example.com/ee-admin/) to see available tools.

![](https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd445b73.jpg) 

_source: EasyEngine_

With the Database name, username & password now you can hence login to PHPMyAdmin

### Deleting a website

To delete a website simply run 

    ee site delete example.com

![](https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd4d29e3.jpg) 

### Restarting Docker Containers

Sometimes due to some bug or high traffic, Nginx may crash: you can simply restart the containers by running

    # Restart all containers of site 
    $ ee site restart example.com 
    
    # Restart single container of site 
    $ ee site restart example.com

Those were just some of the things you can do with EasyEngine, it is a very powerful tool: easy and quick. They have every command laid out well documented on their [website](https://easyengine.io/commands/).

[EasyEngine Github](https://github.com/EasyEngine/easyengine)