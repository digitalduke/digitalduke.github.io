---
layout: post
title: What is DoH and how to cook it?
commentIssueId: 35
---

The dark times are coming... Threats of confidentiality and privacy on the Internet become more serious day by day. There are many ways to secretly harvest and track our personal data and data about behavior in the network, for example to sale it. The even bigger problem is that intruders or not honesty ISP's or government structures can be spoofing our requests to the sites and divert traffic to other resources. For censorship purposes or for scamming.

How they can do it? I'll try to explain. There are three big whales on which the Internet stands on: TCP/IP, DNS, and BGP. Let's see how one of these works. How all we know all sites have their unique names, such as _github.com_ or _stackoverflow.com_ and so on. But they are for humans not for machines and network devices. Network devices are working with IP addresses, like this `1.1.1.1` or this `140.82.118.4` These addresses are hard to remember. That's why we have a Domain Name System or DNS.

What going on when you type *github.com* in the address bar in your browser? Your browser needs to know where to find it on the Internet. He asks a DNS service to resolve the name *github.com* and DNS returns his *IP address*.

```
- You don't know how to get to the wikipedia.com? 
- Oh, yes, just go to 208.80.154.232
```

How does browser find DNS service? He asks operating system about it. 

```
- Can you help me? I need a resolver.
- Of course! I use this resolver.
```

How does an operating system know about resolver? There are two ways. You may configure a specific resolver to which you trust. But if you don't do this, by default it will be using any resolver that comes from a network. When you connect your device to a network (laptop, or smartphone and so on) this device receives an IP address from network equipment, and in addition, address of preferred DNS server(s). 

And this is a problem. Even if you configured your preferred DNS server. Because the DNS protocol does not have any security. Questions and answers (queries) between your device and DNS service can be tracked or spoofed. Network devices of ISP's, such as routers, for example, can read DNS queries without any problem. Also, they can manipulate them. We are under risks and often don’t know about it.

Luckily there is the technology to prevent it - its name is [DNS over HTTPS (DoH)](https://tools.ietf.org/html/rfc8484). It encapsulates DNS queries into secured and encrypted HTTPS requests. As a result, these queries become encrypted and confidential. Already now you may start to use it. It supported by giants such as Google, Mozilla, Cloudflare and so on. This is yet young technology but I recommend to start using it.

If you use Firefox, ensure that you have version 62 or above. Go to the menu, choose **Tools**, and then **Preferences**. Go to the **General** section and into the **Network Settings**. Select *Enable DNS over HTTPS*, then types DoH resolver address. If you prefer Mozilla products you may use *https://mozilla.cloudflare-dns.com/dns-query*.

If you use Chrome, for now, you may turn on this feature via command line: 

```shell
$ /usr/bin/google-chrome-stable --enable-features="dns-over-https<DoHTrial" --force-fieldtrials="DoHTrial/Group1" --force-fieldtrial-params="DoHTrial.Group1:server/https%3A%2F%2F1.1.1.1%2Fdns-query/method/POST"
```  

Finally, visit [https://1.1.1.1/help](https://1.1.1.1/help) to ensure that your DNS queries are now encrypted. You will see something like this: 

![image](https://user-images.githubusercontent.com/36848305/62159626-98cc4400-b32b-11e9-9393-847c8bad8db0.png)

And this is good!

P.S.: for mobile devices, there are also brand name apps from Cloudflare for [iOS](https://itunes.apple.com/us/app/1-1-1-1-faster-internet/id1423538627) and [Android](https://play.google.com/store/apps/details?id=com.cloudflare.onedotonedotonedotone). 
