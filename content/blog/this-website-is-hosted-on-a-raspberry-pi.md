+++
author = "Vimarsh"
categories = ["Tech Stack", "Tutorial", "Self Hosting"]
date = 2022-01-24T18:30:00Z
description = ""
images = ["/uploads/2022/06/hostedonrpi-rev1.jpg"]
tags = ["raspberry pi", "cloudflared", "tech", "tutorial", "writefreely"]
title = "This website is hosted on a Raspberry Pi"
url = "/blog/this-website-is-hosted-on-a-raspberry-pi"

+++
Update: This website is now hosted on a server on Oracle Cloud. RPi was being slow.  
 This website, the exact one you are reading right now is hosted on a Raspberry Pi (RPi) that too the original RPi B. In this post I will document why I did that and how.

![The hardworking Raspberry Pi B](/uploads/2022/06/hostedonrpi-rev1.jpg)

## The Stack

* Writefreely //the blogging platform I am using. Extremely simple, minimal, not even images, with markdown support.
* The Raspberry Pi //I had received this RPi B from a contest on Element14. It just has 512 MB RAM, a 16 GB microSD and 1 single core.
* Cloudflare Argo Tunnel //To tunnel the traffic from www to this Pi

_If you want to learn just about the tech part, scroll down_

## But Why?

After much inspiration from [Low Tech Magazine](https://solar.lowtechmagazine.com/power.html) which uses Solar energy, and is hyper efficient; the trend of self-hosting; and my boredom – I decided to do this. I have changed platforms for my website at least 7 to 8 times but I would never publish consistently. I am hoping that with this I just open writefreely and start writing whenever I want to.  
 I also liked the idea, that in this age, we expect everything to always work!. That wasn't the case before, but this consumption cycle and tech in our hands has made us expect just that. So, to challenge that I have hosted this at my home – which might suffer internet outage, power loss. It might not always be up, and I am perfectly fine with that.  
 Almost all modern websites are filled with decoration, images, animations – which are not required. Sure, people enjoy it and that is all amazing. Even though I was tempted to make one, I knew that to focus on writing I needed one to do just that, and nothing more. Also the fact that your website has very little carbon footprint is gratifying.

Secondly, Analytics. I do not like everyone tracking you on the web. Hence, I used to use a self-hosted instance of [Plausible analytics](https://z.0xvimarsh.com/) which I still do for other people's websites. But when I used that, I would constantly check analytics – which country do people come from, of what demographic are the readers, how much time they spent on my website. All of which is not how I wanted me to write content. Writefreely just shows you how many views, each post gets – which is just a pleasure. Simple.  
 I could in theory, get the logs from my Pi, organize the data from user-agent, but that is just too much of work I feel.

## Why Writefreely

I used to first use Blogger, Wordpress, moved to Ghost for some time, then to Google Sites. The previous one I [used](https://notion-based-website.onrender.com/) was just a website which would render from my notion workspace. It was all great. I could type in my thoughts in notion, and viola! it would show up. Although that was probably the longest time I stuck with one platform (almost 4 months), I was just unhappy with its performance. On my 6 year-old phone it took 15 seconds to open the homepage – unacceptable. That was partly due to big chunks of json, js and also the fact that it renders it every time someone visits.  
 I wanted to try something new. Wordpress was first I looked into – it was open source, simple, fast, you can migrate it anywhere. I recommend people to use wordpress most of the time. But for me... I knew if I did that, then I would just fiddle with its themes and not get anywhere.  
 Writefreely seemed like a sweet spot. Easily could write, just a binary, SQLite DB, and can move to any other machine super quickly: without any hastle.

## How?

1. Setting up RPi
   * I firstly flashed a microSD Card with Raspbian Lite (32 bit) using the official utility [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
   * Then connected monitor, ethernet cable, etc and enabled SSH by running `sudo raspi-config`
2. Installing Writefreely
   * Following the official instrucitions [given here](https://writefreely.org/start). Also set-it up as system service, to run on boot.
   * I selected reverse-proxy & SQLite for DB during setup
3. Installing Argo Tunnel
   * Following [Cloudflare's doccumentation](https://developers.cloudflare.com/cloudflare-one/tutorials/share-new-site), I installed Argo Tunnel.
   * I simply ran `cloudflared --hostname www.vimarsh.info http://127.0.0.1:8080` to start proxying traffic.
   * I was contemplating on setting up a VPS and using SSH reverse tunneling, but this was simple, quick and super easy :D

Just like that, the website was up and running on the internet. Lucky for me, notion provides a markdown export, which I could import super easily. This is not a static website, with html files being served. So, it is possible that the RPi cannot handle it, but I am doubtful.  
 For images: I am using a github repo connected to vercel, and for each image, I upload it and embed it here. 

## Conclusion

Overall I am pretty happy with the setup. Hopefully this means, I actually pen down more articles. Currently, if the lights go out – the tunnel isn't going to restart (I haven't set it up yet). I just use a self-hosted [monitoring service](https://github.com/louislam/uptime-kuma) on the cloud which pings me on discord, when the website is down.