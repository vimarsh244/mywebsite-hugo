---
title: How to access your local server without port forwarding
author: Vimarsh
date: 2021-05-12T23:00:00+05:30
url: "/blog/reverse-tunneling/"
images:
- "/uploads/2021/05/12/optimized-jakob-soby-rjpg-_lvmiq-unsplash.jpg"
description: Sometimes because your server is behind a NAT, or port forwarding not
  allowed, or you want a static IP, you could use SSH reverse tunneling to access
  it. A simple guide on how to do same.
categories:
- Tech
- Blog Post a Day
tags:
- firewall
- NAT
- servers
- reverse tunneling
- SSH

---
Sometimes due to several reasons as mentioned above along with some firewall restrictions, you cannot directly port forward your application. There are several tools like [ngrok](https://ngrok.com/), [Cloudflare Argo Tunnel](https://www.cloudflare.com/en-in/products/argo-tunnel/) that try to do similar things. But either its setup requires a lot of setup or it is that I wanted to not rely on any such service.

In this instance, I had a windows server at home which I wanted to be accessible from anywhere so that I could access it. I tried 10-15 days of exclusively using it as a remote machine and it was a weird experience nonetheless (blog post to come soon).

I decided to finally get a remote server on some reliable cloud provider and use SSH reverse tunneling to forward all my RDP traffic.

> Reverse SSH tunneling allows you to use that established connection to set up a new connection from your local computer back to the remote computer.
>
> Because the original connection came _from_ the remote computer _to_ you, using it to go in the other direction is using it “in reverse.” And because SSH is secure, you’re putting a secure connection inside an existing secure connection. This means your connection to the remote computer acts as a private tunnel inside the original connection.
>
> \- [howtogeek.com](https://www.howtogeek.com/428413/what-is-reverse-ssh-tunneling-and-how-to-use-it/ "Howtogeek link on the topic")

**Step 1**

The first step is to get a remote sever with a publicly accessible IP (preferably static, at least in my case). I also wanted the cost to be as minimal as possible with the highest uptime. Hence, I decided to use [Digital Ocean](https://m.do.co/c/32b907edbd54 "Digital Ocean") (referral link - get $100 to use for 2 months) because of simple and transparent pricing as regional datacenter.

For more simplicity (but definitely a huge security issue) you could allow all traffic in firewall configuration. DO NOT DO IT. plz

**Step 2**

The next step is to login to your VM and add the following commands to `/etc/ssh/sshd_config` file (make sure to take a copy before modifying)

Using vim or nano or any text editor that came built with your distro of choice add or uncomment the following lines.

    GatewayPorts yes
    ExitOnForwardFailure yes

This command basically enables ability to tunnel traffic via SSH connection. [More details](https://www.ssh.com/academy/ssh/tunneling/example). The second line makes sure that incase the tunnel gets shut down, the port is freed up as often when you restart the tunnel, it won't as it will give error for port in-use as SSH still thinks something is connected to it.

**Step 3**

_On Windows_

Simply download your favourite SSH client utility, I prefer [Putty](https://www.putty.org/ "Putty"). In the same folder the putty exe is placed, run the following for forwarding RDP traffic to post 12345

    .\putty.exe -ssh -R 12345:localhost:3389 root@<ip address> -pw <Your password>

It is better to use key exchange for authentication, but I believe with a really strong password and after changing default SSH port, it is not that big of a concern (at least for me).

_On Raspberry Pi_

I also do have several services running on my Raspberry Pis and because my ISP has put me behind a [NAT](https://en.wikipedia.org/wiki/Network_address_translation "Wikipedia Page for NAT"), I am unable to access it from outside, hence used this technique.

    ssh -R 5000:localhost:8000 root@<ip address> -pw <password>

**My Experience**

Ngrok and Cloudflare argo tunnel (along with Cloudflare [access](https://www.cloudflare.com/en-in/teams/access/)) are probably a better easy to use solutions, but biggest problem with such solutions is they do not allow traffic like that of remote desktop connection or even UDP for that matter. Also, if there is a lot of traffic flowing through, the costs can rise pretty quickly and hence, would suggest this.

There are definitely better user friendly and arguably even more stable OSS like [Boring Proxy](https://github.com/boringproxy/boringproxy "Boring Proxy Github"), which I have tried and really liked. But this works for me now and works really well. If there isn't a random internet outage I have easily got 100% uptime, which is really good.

This might be a very non-polished solution, but I enjoy using it and it works for me. Also I can host several services on just one droplet. With nginx even using domains is easily possible without the need of different ports for all services. Also if you are testing a new project it is just super easy to make it available without fiddling with router settings every time.