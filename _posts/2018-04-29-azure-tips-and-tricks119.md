---
layout: post
title: "Azure Tips and Tricks Part 119 - Determine the outbound IP addresses of your Azure App Service"
excerpt: "Learn how to determine the outbound IP addresses of your Azure App Service"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Determine the outbound IP addresses of your Azure App Service

Because some networks are locked down and only allow whitelisted IP addresses, I hear these questions a lot. 

* What is my Azure Web Apps outbound IP address?
* What IP addresses do I need to whitelist?

### Question 1

For an individual Azure Web App, you can simply go to the **Properties** of the application:

<img style="border:3px solid #021a40" src="/files/azoutbound1.png">

You can click the copy button to add them to your clipboard. 

### Question 2

If you need to whitelist a region, I first lookup to see what region it is currently deployed in. You can find this information from the **Overview** page of the application. 

<img style="border:3px solid #021a40" src="/files/azoutbound2.png">

Microsoft provide a list of the [Azure Data Center IP ranges in XML format](https://www.microsoft.com/en-us/download/details.aspx?id=41653)

So download this file and search for your region and now you know what IP address to whitelist. 

<img style="border:3px solid #021a40" src="/files/azoutbound3.png">

I hope this helps.


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 