---
title: How to host a WordPress website on a VM simply
author: Vimarsh
date: 2020-11-27T15:10:00+00:00
url: /blog/how-to-host-a-wordpress-website-on-a-vm-simply/

---
 

  * Create a Ubunutu 20.04&nbsp;VM
  * Run the following commands via&nbsp;SSH<figure class="wp-block-image">

![][1] </figure> 

<pre class="wp-block-code"><code>sudo apt-get update && sudo apt-get upgrade -y

wget -qO ee rt.cx/ee4 && sudo bash ee

sudo ee site create website.com –type=wp –admin-user=admin –admin-pass=password

sudo ee site update website.com –ssl=le
//for SSL

</code></pre>

 [1]: https://vimarsh.info/wp-content/uploads/2021/02/img_6022bb96ed1a7.gif