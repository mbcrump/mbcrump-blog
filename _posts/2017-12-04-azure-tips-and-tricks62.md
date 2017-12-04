---
layout: post
title: "Azure Tips and Tricks Part 62 - Force HTTPS in Azure Functions"
excerpt: "Learn how to force HTTPS in Azure Functions"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Force HTTPS in Azure Functions

I was looking into adding HTTPS to an existing Azure Function that I had and was pleasantly surprised that you can easily do this now through the Azure Portal (and I assume CLI). Simply log into the portal and select your Azure Function, go to **Platform Features** and then click on **Custom Domains** as shown below: 

<img style="border:3px solid #021a40" src="/files/azhttpsblog1.png">

This will bring you to the **Custom Domains** page and here you can switch HTTPS to On and either add a hostname or domain name. Keep in mind that you don't have to actually add a new hostname/domain to use this feature. 

<img style="border:3px solid #021a40" src="/files/azhttpsblog2.png">

<img style="border:3px solid #021a40" src="/files/azhttpsblog3.png">

**What if users are accessing my HTTP version?** They will receive a 301 Status code and be redirected to the HTTPS site.
{: .notice--primary}

Now secure those Azure Function sites! :) 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 