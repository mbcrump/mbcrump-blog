---
layout: post
title: "Azure Tips and Tricks Part 44 - Deploying Azure Logic App through Visual Studio 2017"
excerpt: "Learn how to use Visual Studio 2017 to deploy an Azure Logic App"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Deploying Azure Logic App through Visual Studio 2017

Now that you know [how to setup your Visual Studio environment](http://www.michaelcrump.net/azure-tips-and-tricks43/), you probably wrote some code and it is time to deploy it. 

Fire up Visual Studio 2017 Logic App project. In my case, I created an app that would monitor tweets and post them to OneDrive, but you can do whatever you want.

<img style="border:3px solid #021a40" src="/files/vs2017deploylogicapp1.png">

Right click on the name of your project and select **Deploy** and then either **New** or an existing resource group. 

<img style="border:3px solid #021a40" src="/files/vs2017deploylogicapp2.png">

It will prompt you to login, so do so now. 

<img style="border:3px solid #021a40" src="/files/vs2017deploylogicapp3.png">

If there are any fields that you missed, then it will prompt you to enter them now. In my case, I had not set the name and it prompted me to do so. 

<img style="border:3px solid #021a40" src="/files/vs2017deploylogicapp4.png">

Now you'll see in the output window that it calls the PowerShell script to deploy the resources for your Logic App. 

<img style="border:3px solid #021a40" src="/files/vs2017deploylogicapp5.png">

Once it finishes deploying, log into the Azure Portal to see your new resource. 

<img style="border:3px solid #021a40" src="/files/vs2017deploylogicapp6.png">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 