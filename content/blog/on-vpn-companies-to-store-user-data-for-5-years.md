---
title: On VPN companies to store user data for 5 years
author: Vimarsh
date: 2022-05-7
url: "/blog/on-vpn-companies-to-store-user-data-for-5-years"
images:
- "/from-temperory-writefreely-blog/chris-yang-1tnS_BVy9Jk-unsplash.jpg"
description: There has been a big spur in media, on social networks and forums (not in local newspapers) regarding new directive from Indian Computer Emergency Response Team (CERT-In). All the focus has been on a specific thing, being that VPN companies storing user data for 5 years. 
categories:
- Thoughts
- Tech
- Freedom
tags:
- philosophy
- thoughts
- India
- Policies

---
So, here is everything regarding this [new directive](https://www.cert-in.org.in/PDF/CERT-In_Directions_70B_28.04.2022.pdf).

There are a lot of bad opinions but also misinformation which I will not be correcting but here is what it says. [Backup PDF for same](/from-temperory-writefreely-blog/CERT-In_Directions_70B_28.04.2022.pdf)
First it is quite important to clear up that this is regarding cyber threats only i.e., trying to figure out threat actors for cyberattacks and overall ensuring India's cyber well-being.

![A person standing in front of a display—looks like a hacked computer screen](/from-temperory-writefreely-blog/chris-yang-1tnS_BVy9Jk-unsplash.jpg)

## What does it say?

1.. All service providers (private and government bodies) must use computer time that is derived from NTP operated by Indian research institutes (NPL, NIC). This is quite critical because all financial transactions, a simple WhatsApp message, etc. requires the clocks to be synced and in case of any disaster/war a reliance on a foreign server is not ideal. All secure communications over internet (the padlock in your browser right now) relies on accurate time, and using a local instance is crucial for sovereign security.

Just running my own DNS server, I got to know that my phone pings US NTP servers for time with no obvious way to change it in phone settings.

2.. All major organizations should report the existence of any security vulnerability or attack to CERT-In within 6 hours of identifying. Pretty reasonable, although time is a little less. Also, does 'body corporate' include compromise of a small-scale website operated by a small company? Clarifications would be helpful.

3.. The mentioned 'service provider/intermediary/data centre/body corporate' are required to appoint a Point of Contact personal which CERT-In would contact for getting information regarding cyber incident and help in its resolution.

4.. All these entities need to enable rolling logs for their systems and store it for 180 days. Which kinds of logs – IP addresses, TCP packets, type of program being run?? None of it is mentioned, making it very vague and confusing. 

5.. Data centres, VPS providers, Public Cloud providers (AWS, GCP, etc.) & VPN companies must store logs regarding user details, IP addresses allocated & at what time, verifying address, contact details, email, etc. More importantly, for 5 years even after user has terminated their service!!!

Foremost, how will these companies like Digital Ocean, GCP,  NordVPN, ProtonVPN verify address. Will they start asking for PAN / Aadhaar details!? Secondly 5 years is a very loooong time for storing logs like these. The decision seems to be in good faith of knowing who caused a DDoS attack / credential stuffing on an important government portal, but 5 years is completely unnecessary. 

If you are requiring for details of a security incident in 6 hours, why not follow up with just telling to store these logs for let's say a week and hence trying to resolve issues as quickly as possible. For Public cloud providers it does make sense but VPN providers? 
People use VPNs simply to be anonymous & it is not always just bad actors using it—Journalists, Reporters, even government officials need anonymity to protect themselves from internal or external actors. Trying to combat a few bad actors will hinder the safety of these people and India's security & democracy. Does it mean ISPs will be required to block IPs of VPN companies not based in India? None of it is clear and it seems to me that actions will not be taken; only time will tell.
Might write a blog on simply setting up your own VPN in a foreign jurisdiction.

The EU with its GDPR directive allows users to request companies (including these cloud providers) to completely delete all data once whenever they request BY LAW. And here we are allowing these companies to keep data BY LAW. It is a horrible decision and I hope it is changed.

6.. It's regarding crypto - whoooo! All custodian wallet providers (coinDCX, wazirX, etc.) will be required to do KYC verification of its users and record public addresses of funds transferred to / from and more. It says – '... accurate information shall be
maintained in such a way that individual transaction can be reconstructed ...' All governments seem to want to do this as crypto is considered alien, although this will just scare away crypto devs to other jurisdictions hindering our own progress—yay!

## Vagueness

The entire directive is quite vague with no justifications or how it will be followed up. CERT-In does [seem to](https://www.cert-in.org.in/) maintain CVEs, but that's pretty much it.

The list of incidents for which reports must be made to include things like Data Breaches and Data leaks. This is fantastic —considering a lot of companies just hide any breach that has occurred until it gets dumped on the web. Hopefully the 6-hour reporting works!? 
But it also has weird keyword overload of Big Data, Blockchain, Artificial Intelligence for which threats seem really weird. 

It might stop small actors DoS-ing a state government's portal, but will not affect any big threat actor.
It also does not mention open source maintainers to comply which is good, but a lot of CVEs are for open source packages like the recent log4j or many in Mozilla Thunderbird / GitLab (currently on CERT-In's own front page) and there is no instruction on how government bodies / contractors should treat it.


## In Conclusion

The directive seems to be in good faith and luckily does not mention most consumer side apps / services, which is good (except the unusual VPN thing). It also seems to be extremely vague and unenforceable until it's some serious data breach (like of Aadhaar details or something). 

The direction is good with asking bodies to use NTP maintained by India. Although we do need more maintainers for [Indian NTP pool.](https://www.pool.ntp.org/zone/in)
I would rather wish there were more directives for protecting consumer data, especially from foreign nations—something like the GDPR (but without the cookie consent mess). Basically asking any company with revenues over $10 million to store data of Indian users in India.

They mention reporting of cyber issues, but what are the plans to address it and prevent from occurring remain unknown. 

### Random thoughts

Also, there has been a lot of misinformation on Indian users losing privacy and government being able to request all data about what you type in G docs, and things like that. Which is simply untrue. I am not going to list and correct many such articles / forum posts / YouTube videos here.

It will also be very interesting on which VPN providers still do operate in India after 27 June – the no log policy will really show itself. The companies do have a lot of investments already done in marketing; will they let go off them or comply is to be seen.