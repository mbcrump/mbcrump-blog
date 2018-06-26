---
layout: post
title: "Azure Tips and Tricks Part 135 - Use Run-From-Zip without Azure Storage to deploy a site to Azure Web Apps or Functions"
excerpt: "Learn how to use Run-From-Zip to deploy a site to Azure Web Apps or Functions with Azure Storage"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use Run-From-Zip without Azure Storage to deploy a site to Azure Web Apps or Functions

[Yesterday](http://www.michaelcrump.net/azure-tips-and-tricks134/) I discussed a feature that gives you the ability to deploy a site to Azure Web Apps or Azure Functions from a zip file. It is called **Run-From-Zip** which you simply point to the location in your App Settings and it automatically gets mounted on wwwroot as read-only. 

The one requirement that it had was that you need an Azure Storage Blob Container. If you don't want to do that than an alternative approach is to host the files on Kudu. 

Open Kudu and create a `home\data\SitePackages` folder, and drop your zip file in there. 

<img style="border:3px solid #021a40" src="/files/azkudu1.png">

Create a file named `packagename.txt` and give it the name of your zip file. 

Mine looks like the following `mcsample.zip`

In **Azure App Settings**, set `WEBSITE_RUN_FROM_ZIP` to `1` instead of the full path that we used yesterday with Azure Storage Blob Container. 

Just like yesterday, give your site a couple of seconds and you should see your site that was deployed via a zip file from Kudu. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 