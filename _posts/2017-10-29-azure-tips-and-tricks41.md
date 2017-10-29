---
layout: post
title: "Azure Tips and Tricks Part 41 - Quickly Roll Back to a Previous Version of an Azure Logic App"
excerpt: "Learn how to quickly roll back to a Previous version of an Azure Logic App"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Quickly Roll Back to a Previous Version of an Azure Logic App

This one seems to come up a lot, so I'll add it here. If you have created an Azure Logic App and would like to go back to a previous version, then you can do so very easily. Go ahead and open your logic app and look under **Development Tools** then **Versions** and select a previous version. 

<img style="border:3px solid #021a40" src="/files/versionlogic1.png">

Once you select a previous version, you'll see **History**.

<img style="border:3px solid #021a40" src="/files/versionlogic2.png">

From here you can hit the **Promote** button and **Save** to use this version in production. 

**Remember this!** Keep in mind that this isn't an alternative for using Source Control (like GitHub). It is just a nice thing to know when experimenting with Logic Apps.
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 