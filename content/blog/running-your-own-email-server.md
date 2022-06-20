+++
author = "Vimarsh"
categories = ["Self Hosting", "Tutorial"]
date = 2022-02-10T18:30:00Z
description = "Email was one of the earliest services for communication via the internet. But, hosting such a simple service is quite complicated nowadays. In this post I have documented how I set up an email server for a business quickly and easily."
images = ["/uploads/2022/06/stephen-phillips-hostreviews-co-uk-3mhgvrk4tjm-unsplash.jpg"]
tags = ["self hosting", "email", "tutorial", "tech", "server"]
title = "Running your own email server"
url = "/blog/running-your-own-email-server"

+++
## Why would someone need that?

There already exists several established players for simply sending and receiving emails, but there could be reasons why you would want to host your own: – Privacy If you are dealing with financial data, or in general don't want Google, Microsoft, etc. to snoop in over your emails – Several Users If you have more than a couple users on your domain name, hosting emails gets expensive, and that too quickly. Hosting it on your local server or a VPS is much cheaper than paying for GSuite if not using its other services. – Control The Internet is becoming quite centralized especially with messaging (WhatsApp, Signal, iMessage, etc.). Email by its virtue is meant to be distributed making it ideal for messaging. \[Will talk about encryption further\]

![Gmail's UI on a laptop screen](/uploads/2022/06/stephen-phillips-hostreviews-co-uk-3mhgvrk4tjm-unsplash.jpg)

## Choosing an email server

Upon quick googling we can find that there are [several email server solutions](https://github.com/awesome-selfhosted/awesome-selfhosted#communication---email---complete-solutions). Basically a complete package that is easy to run and maintain. After a lot of testing of different solutions and checking feature parity, I decided on using [Power Mail-in-a-Box](https://github.com/ddavness/power-mailinabox) {a fork of [Mail-in-a-box](https://mailinabox.email/) — an already popular solution} for setting it up for a business. A couple of reasons for choosing it, over several others:

* Supports Ubuntu 20.04, Debian 10/11 out of the box. This means that at least for several years, no major upgrades or maintenance will be needed.
* Pretty lightweight: can run on a 1 core CPU with 1 GB ram (a cheap Digital Ocean VM)
* Supports email routing, aliases, email forwarding, etc.
* Has support for an external SMTP relay. As you might know, a lot of Cloud providers and ISPs block port 25 (for outgoing email) or the IP is already blacklisted. Getting a clean IP, and convincing your ISP to setup [reverse DNS](https://mailinabox.email/guide.html#:\~:text=option%2C%20disable%20it.-,Reverse%20DNS,the%20reverse%20DNS%20of%20your%20box%20to%20your%20box%E2%80%99s%20hostname.,-If%20you%20are) is super difficult. \[more on this later\]
* Support for OpenPGP based native email encryption.
* Allowing to set up usage quotas for different users.
* Support for backup natively via rsync, Back blaze, locally and also on S3 storage.
* Has support for calendar and contacts sync. Also has built in Nextcloud for users to store some files and share.

P.S. By default, all emails sent to the same domain are just routed internally.

## Hosting

There are several ways to host your email server. The best is to just repurpose any old system, with a replaced drive, adding ram, etc.

**An old system's specs which I tested everything on** – An Old system with intel i3-2100 or something – 6 GB DDR3 RAM – 500 GB WD Blue SSD (\~60 USD) //added extra

You can also deploy on a cloud provider, which I did for the business this was set up for. I recommend [Digital Ocean (affiliate link)](https://m.do.co/c/32b907edbd54) simply because it's super simple, doesn't block ports and setting up reverse DNS is just as simple as renaming your VM. Although you need to get lucky with an IP that is not blacklisted.

## Setting everything up

After installing the OS, setting it up is literally super simple. Follow the steps on the [GitHub readme](https://github.com/ddavness/power-mailinabox#installation). You will need to configure port forwarding on your router if hosting locally or in your cloud provider's firewall settings.

I would **not** recommend setting up your box as the DNS server, because if it goes down, your website and even other services will not be accessible publicly. I would hence recommend just copying all records shown and adding it to your DNS server (Cloudflare, Route 53, etc.)

![Setup DNS on an external provider](/uploads/2022/06/external-dns-power-mailinabox.png)

You might not want to open outgoing ports or if ISP might be blocking outgoing email ports (esp. 25), continue reading ahead for a simple solution.

## Email Deliverability and SMTP relays

There are several reasons why your emails will be ending up in spam. In fact, you might not even be able to send emails if your ISP is blocking specific ports. For these reasons, SMTP relays come into play.

Basically all your emails from your server are sent to another service which then delivers the email from their servers, which are not blacklisted, ensuring perfect delivery. The emails someone else sends are still delivered to your mailinabox; just sending is handled by such an SMTP relay.

There are several services like AWS SES, Sendgrid, etc. but I really liked [Zoho ZeptoMail](https://www.zoho.com/zeptomail/) due to its simple pricing (\~ $2 for 10,000 emails), amazing email delivery, and very good customer support which approved our account fairly quickly. There are also several free services like Sendinblue, Mailazy, etc. if sending very few emails/day. After you make an account, setup the required DNS records for your domain; you can configure it in the admin interface as shown below:

![PowerMail-in-a-box configure SMTP relay](/uploads/2022/06/setting-up-smtp-relay.png)

## Encryption

As I alluded to earlier, you might want privacy and prevent Tech Giants, ISPs from snooping in on your emails. There exists simple solutions like [Proton mail](https://protonmail.com/) to encrypt your emails end-to-end but self-hosting email takes it to another level. Power Mail-in-a-box supports OpenPGP based email encryption and decryption in Roundcube (webmail) itself. It basically ensures that no one can read an email which is sent to you with your public key, and the emails you send could also be encrypted and signed to prove that they are not spoofed. Pretty cool!

## Conclusion

Even though I set this up for a business because the [free GSuite days are coming to an end](https://support.google.com/a/answer/60217), I would not do it for myself. Managing infrastructure is still work, even though mail-in-a-box basically requires almost zero maintenance after everything is configured. For me, I just use Zoho Mail which gives 5 GB free for 5 users on a custom domain, which is generous for individuals & family.

But, for small sized organisations or just for having some fun, this is a legitimate and extremely simple way to set up a mail server. With SPF, DKIM records properly configured and using a relay, even email deliverability is not an issue. The install which I did has been stable and running for a month almost. I will highly recommend setting up backup — its super simple. It supports rsync directly to another remote machine via SSH keys, and it can be configured via the web admin interface itself.

Thanks to [Aryan](https://aryantiwari.com/?utm_source=vimarsh) for reviewing this article