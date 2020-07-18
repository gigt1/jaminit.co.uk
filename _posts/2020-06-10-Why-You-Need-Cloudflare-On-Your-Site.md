---
categories: [Websites]
tags: [Cloudlflare, Speed, Website Speed]
---
So, you’re probably here because you’re on the fence to deciding wether to take the leap and use Cloudflare. Well before I go and tell you all the reasons for using Cloudflare lets talk about the very few reasons when you shouldn’t and might not want to.


**NOTE: This port was ported over from my old WordPress blog appologies if any of the links are broken**

## When You Shouldn’t Use Cloudflare:

* For people who don’t know about changing nameserver’s and dns records. If you are thinking about switching to Cloudflare and you don’t know what these are you should first either educate yourself on these or simply don’t do it. These are two fundamental concepts you should know about before proceeding
* If you don’t want to deal with the hassle of occasional debugging.

## When You Should Use Cloudflare:

Now the part where I tell you when you should use Cloudflare
### To Speed up Your Website:

Cloudflare’s main USP is a CDN, what this means is that it caches your site around the world. This means when your client requests your site, the datacentre serves your site from the closest location to them instead of going all the way to your server.

![Diagram of bounce rate](/images/BounceRateGoogle.jpg)
Above: a diagram showing the probability of bounce rate

The diagram above shows that the slower your server is at loading your page the more likely visitors are simply going to get bored of your site loading and move onto something else.
### Ease of Setting Up New Subdomains:

* Cloudflare also hosts your DNS records and because of this you don’t need to wait for the average 24-48 hours your registrar takes to add your DNS records, you can just simply create the subdomain and add the dns records in cloudflare. This means if you need to suddenly redirect website vistors to a different server because of a Ddos attack you can do it in seconds instead of hours.

### Protection:

You’ve probably heard of websites getting “DDosed” (Distributed Denial of Service). It’s basically where attackers keep pinging your server with 1000’s of requests a second until your server simply cannot cope anymore and crashes. An advantage of using Cloudflare is that they protect your servers from being DDosed.

![Diagram of bounce rate](/images/DDos-Page.gif)
Above: Cloudflare protecting a site from a DDos attack

### It’s FREE:

* Yeah, you heard me right. Cloudflare has a free unlimetered bandwidth plan. It means you can use it with unlimetered DNS records and unlimetered people visiting your website. You can also get access to Cloudflare Service workers which enable you to run your JavaScript code on servers around the globe at lightning fast speed.
## Overall:

In conclusion if you know how to setup Cloudflare I strongly recoment that you do since it makes everything so much easier, secure and speedy. I personally use it on this site and my clients website and it speeds everything up massively. I’m going to be doing a blog post on caching plugins for WordPress in a short while so make sure you don’t miss that!
