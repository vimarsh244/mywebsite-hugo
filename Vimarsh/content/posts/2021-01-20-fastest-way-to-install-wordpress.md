---
title: Fastest way to install WordPress
author: Vimarsh
date: 2021-01-20T15:10:00+00:00
url: /blog/fastest-way-to-install-wordpress/
featured_image: /wp-content/uploads/2021/02/1_1hLHDT7VkTYf0vWKdQhvcHA.png

categories:
  - Tutorial

---
 

I will be showing you the fastest way to install a fully functional WordPress website with an auto-renewing free SSL certificate in less than 3 commands. Let’s get&nbsp;started.

### Prerequisites 

Make sure you are using Linux or Mac for installing WordPress. If you are deploying a website you might be using a virtual machine in the cloud for the same. _Stay tuned for another post on how you can get 2 free VMs forever on Oracle&nbsp;Cloud_

We will be using an open-source tool called [Easyengine][1] for installing and managing WordPress.<figure class="wp-block-image">

![][2] </figure> 

<blockquote class="wp-block-quote">
  <p>
    <em>EasyEngine makes it greatly easy to manage Nginx, fast web-server software that consumes little memory when handling increasing volumes of concurrent users.</em>
  </p>
</blockquote>

### Let’s get&nbsp;started<figure class="wp-block-image">

![][3] </figure> 

### SSH into the&nbsp;VM

You can use Putty / Powershell or Terminal to SSH into the&nbsp;VM

Also, make sure to update installed packages by running sudo apt-get update && sudo apt-get upgrade&nbsp;-y

### Install EasyEngine

Run the&nbsp;command

<pre class="wp-block-preformatted"># Install EasyEngine on Linux
wget -qO ee rt.cx/ee4 && sudo bash ee

# If installing EasyEngine on Mac for Local Development brew install easyengine</pre>

### To install WordPress website run the&nbsp;command

<pre class="wp-block-preformatted">sudo ee site create website.com</pre>

You can change the username & password of the WordPress install for security when you first open the&nbsp;website.

**Make sure to change** [**website.com**][4] **with your domain&nbsp;name**

I also recommend setting up Redis cache for a better performant website ee site create example.com &#8211;type=wp &#8211;mu=subdir &#8211;cache

Easyengine automatically creates the database, sets up secure username and passwords as well. Making the whole process super&nbsp;easy.

<blockquote class="wp-block-quote">
  <p>
    <em>Currently Easyengine does not support running without root privileges.</em>
  </p>
</blockquote>

You can check out further options&nbsp;[here][5]

### Pointing the domain name to the&nbsp;server

Make sure you point your domain name to the server’s IP&nbsp;Address

Go to nameserver provider and set A record for your&nbsp;server.<figure class="wp-block-image">

![][6] </figure> 

**DNS Propogation might take&nbsp;time**

### Registering a SSL certificate

To get auto-renewing _free_ SSL certificate run

<pre class="wp-block-preformatted">sudo ee site update website.com</pre>

This will install an SSL certificate from [Let’s Encrypt][7] and change necessary database entries for HTTPS. The certificate also auto-renews 1 month before the&nbsp;expiry

_This might not work properly with Cloudflare_

**And that is all.** You have a fully functional WordPress website with auto-renewing SSL certificate. You can go to the WordPress admin panel [example.com/wp-admin][8] and start customizing.

_And you can also create more websites on the same&nbsp;instance_

### Some other Useful&nbsp;Commands<figure class="wp-block-image">

![][9] </figure> 

<blockquote class="wp-block-quote">
  <p>
    <em>Make sure to run with root privileges. You can use </em><em>sudo su to run all following commands as&nbsp;root</em>
  </p>
</blockquote>

### Installing PhPMyAdmin

Easyengine gives the option to enable PhPMyAdmin and other admin&nbsp;[tools][10]

To use that run ee admin-tools enable example.com

By default, http authentication will be enabled. To view the username & password run ee auth list&nbsp;global

Then you can go to [example.com/ee-admin][11] to see available tools.<figure class="wp-block-image">

![][12] </figure> 

_source: EasyEngine_

With the Database name, username & password now you can hence login to PHPMyAdmin

### Deleting a&nbsp;website

To delete a website simply run ee site delete example.com<figure class="wp-block-image">

![][13] </figure> 

### Restarting Docker Containers

Sometimes due to some bug or high traffic, Nginx may crash: you can simply restart the containers by&nbsp;running

<pre class="wp-block-preformatted"># Restart all containers of site $ ee site restart example.com # Restart single container of site $ ee site restart example.com</pre>

Those were just some of the things you can do with EasyEngine, it is a very powerful tool: easy and quick. They have every command laid out well documented on their&nbsp;[website][14].

[EasyEngine Github][1]

_Originally published at_ [_https://blog.vimarsh.info_][15]_._<figure class="wp-block-image">

![][16] </figure>

 [1]: https://github.com/EasyEngine/easyengine
 [2]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd2afa4f.jpg
 [3]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd33e0d4.jpg
 [4]: http://website.com
 [5]: https://github.com/EasyEngine/site-type-wp
 [6]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd38c086.jpg
 [7]: https://letsencrypt.org/
 [8]: http://example.com/wp-admin
 [9]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd3ebd94.jpg
 [10]: https://easyengine.io/handbook/admin-tools/#list-of-admin-tools
 [11]: http://example.com/ee-admin/
 [12]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd445b73.jpg
 [13]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd4d29e3.jpg
 [14]: https://easyengine.io/commands/
 [15]: https://blog.vimarsh.info/fastest-way-to-install-wordpress
 [16]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bbd53dbb4.gif