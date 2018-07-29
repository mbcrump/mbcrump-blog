---
layout: post
title: "Azure Tips and Tricks Part 144 - Swiftly understand what versions of .NET are supported on Azure App Service"
excerpt: "Learn how to swiftly understand what versions of .NET are supported on Azure App Services"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Swiftly understand what versions of .NET are supported on Azure App Service

With the release of .NET Framework 4.7.2, I've been asked multiple times it Azure App Services (Websites) supports it yet. While I can quickly answer this question, there will always be a vNext and this question may come up again. So how do you check to see what version of the .NET Framework Azure App Services Supports? 

One of the easiest ways that I know of it to use an existing website that you created that is hosted on Azure App Services and go to the **Development Tools** and **Advanced Tools** and open the Kudu Portal

<img style="border:3px solid #021a40" src="/files/azureappkudu1.png">

Then to go the **Debug console** and then **CMD**. 

<img style="border:3px solid #021a40" src="/files/azureappkudu2.png">

Type `cd D:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETFramework` 

You'll see a list of the supported .NET Frameworks! 

<img style="border:3px solid #021a40" src="/files/azureappkudu3.png">

I hope this helps someone out there! 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 