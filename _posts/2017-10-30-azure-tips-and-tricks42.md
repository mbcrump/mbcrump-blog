---
layout: post
title: "Azure Tips and Tricks Part 42 - Modifying an existing API Connection with Azure Logic App"
excerpt: "Learn how to quickly modify an existing API connection with Azure Logic App"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Modifying an existing API Connection with Azure Logic App

If you have created an Azure Logic App, and have an existing API Connection that you would like to modify, then you can do so very easily. Go ahead and open your logic app and look under **Development Tools** then **API Connections** and you'll see a list of API connections associated with the logic app. 

<img style="border:3px solid #021a40" src="/files/logicappconn1.png">

Under **General**, you'll see **Edit API Connection**.

<img style="border:3px solid #021a40" src="/files/logicappconn2.png">

Now you can edit the API information and then press **Authorize** to change the API connection associated with your Logic App. 

<img style="border:3px solid #021a40" src="/files/logicappconn3.png">

**Remember this!** This is good to keep in mind when you might want to test API connections with a personal account before using a production one. 
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 