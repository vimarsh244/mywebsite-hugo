---
title: Why I switched away from Wordpress
author: Vimarsh
date: 2021-05-02T14:00:00+05:30
excerpt: ''
url: "/blog/Why-I-switched-away-from-Wordpress"
images:
- "/uploads/vincent-lavigna-rrevoabucwo-unsplash.jpg"
description: Wordpress is the most popular CMS, and I decided to switch away from
  it to move to Hugo a Static Site Generator.
categories:
- Website
- Tech
- Blog Post a Day
tags:
- frameworks
- Hugo
- SSG
- wordpress

---
Wordpress is the world’s most popular content management system (CMS). It’s estimated that it runs approximately 35% of the entire internet, close to 20 million websites in total. As soon as I got my domain [vimarsh.info](http://vimarsh.info), I knew I wanted to make a website - and Wordpress it was. I had previous experience using it and also had made several Wordpress websites for others. So that is what I did.

Fired up a Virtual Machine and installed Wordpress using Easyengine, also wrote a [tutorial](https://www.vimarsh.info/blog/fastest-way-to-install-wordpress/) on how to do same, and it worked. I was satisfied for almost 3 months, but in the back of my head, I always wanted to do something new. But, my friend convinced myself that wordpress was good enough as it satisfied all my needs to blog and it wasn't like it was hampering my progress in writing. That's when I started to want something better.

I always got notified for new plugins or theme updates almost everyday. Along with that, I had to make sure to take regular backups so that in event of anything going wrong, it would be easy to restore. All that time wordpress would show, website under maintenance, and I seriously did not like that. With all that, I still had to think about SEO and lighthouse scores. I wanted a full score, but would never get. Until now!

![Lighthouse score showing 100 across the board](/uploads/vimarsh-main-website-lighthouse-score.png "Lighthouse score")

How did this happen? Well, I killed Wordpress and moved to static site.

## Wordpress v/s Static Sites

Wordpress is a content management system, based on PhP. Whenever you visit a wordpress website, based on your client screen and resources, the server would render the page and serve it to you. The content for the webpage is stored in a database and hence CMS(es) need to query Database for every request. You could add some caching plugins and a CDN but that added more complexity, which I was trying to avoid. [Ghost](http://ghost.org) is another new cool CMS but I beleive it works on same fundnamental principle.

![Wordpress Plugin Dashboard Image](/uploads/stephen-phillips-hostreviews-co-uk-sspzml7fpwc-unsplash.jpg "Wordpress Plugin Dashboard")

### **What is a static site generator?**

> A static site generator is a tool that generates a full static HTML website based on raw data and a set of templates. Essentially, a static site generator automates the task of coding individual HTML pages and gets those pages ready to serve to users ahead of time. Because these HTML pages are pre-built, they can load very quickly in users' browsers.
>
> \-  [Cloudflare](https://www.cloudflare.com/en-in/learning/performance/static-site-generator/)

At that time I heard about [Static Site Generators](https://jamstack.org/generators/). These are frameworks which build static websites you can host anywhere especially with many free hosting platforms like [Vercel](https://vercel.com/) and [Netlify](http://netlify.app/).

When you get static HTML files, it also gives flexibility to host it anywhere you wish to. Also the time to render the webpage is extremely less as the server does not need to render or prefetch any content. There are technologies like [Next.js](https://nextjs.org/) and [Frontify](https://www.frontify.com/en/) that prerender the webpage even from a database but that is another layer I wanted to avoid. Also, for my use case Wordpress was pretty much an overkill, and also I wanted to play with new developing tech, so that is what I did.

## Why not website builders

A lot of website builders are becoming extremely famous like Squarespace, Wix and Weebly. These are drag and drop super easy to use website builders. Along with that there are platforms like Medium and Substack which are amazing platforms to focus on writing. But my biggest concern with all of the platforms was their future scope. There is nothing stoppping these platforms from increasing prices in the future or downright being bankrupt or changing Terms of Service you might not agree with. For all these reasons, I used and recomended Wordpress, because atleast you could migrate to other hosting platform without fear of Wordpress going anywhere. And SSG are another alternative which bypass such vendor lock-ins.

I also had that weird feeling that what if my blog suddenly blows up, and the server cannot handle the incoming requests. Hence, wanted a solution that could truly scale.

## My choice for SSG

After searching and playing around with several JAMStack Frameworks like [Gatsby](https://www.gatsbyjs.com/), [Next.js](https://nextjs.org/docs/basic-features/pages) (+ React), [jekyll](https://jekyllrb.com/), etc. I selected [Hugo](https://gohugo.io/).

According to their homepage -

![Hugo website homepage](/uploads/hugo-website-screenshot.png "Hugo website homepage")

> The world’s fastest framework for building websites

But for me, the reasons were simple, it was super fast, extremely easy to use and get started with, and had a massive collection of themes with a super friendly community. Along with that, the number of famous websites using it was large and substantial enough for me to not worry that it will vanish the next day.

For theme, I use [PaperMod Theme](https://adityatelange.github.io/hugo-PaperMod/).

With Static Site Generators you have to write in Markdown, which further allows you to easily migrate to any other framework as most of them are based on Markdown. They also allow massive amounts of customisability - from how your page looks to even how links should open in new tab and more.

### The con that is being actively solved

The biggest downside and even the barrier to entry for adoption is the lack of any interface. Wordpress, Squarespace, Ghost, and others provide a really good [WYSIWYG](https://en.wikipedia.org/wiki/WYSIWYG) interface. Although, this downside is addressed by headless CMS like [Netlify CMS](https://www.netlifycms.org/), [Forestry](https://forestry.io/) etc. I personally use Forestry and enjoy doing so. It provides a clean interface which is responsive and super easy to get started with. You don't even need to know any coding to get started with Forestry which is super cool for new users.

**This is how easy it is to create a JAMStack site with forestry.io**

![Getting started with Forestry GIF](/uploads/get-started-with-forestry.gif "Super easy way to create your own JAMStack website")

![Forestry CMS Overview](/uploads/forestry-cms-overview.gif "Forestry CMS Overview")