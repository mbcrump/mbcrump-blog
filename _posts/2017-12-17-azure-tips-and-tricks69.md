---
layout: post
title: "Azure Tips and Tricks Part 69 - Access and embed Azure Cloud Shell Anywhere"
excerpt: "Learn how to access Azure Cloud Shell anywhere"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Access and embed Azure Cloud Shell Anywhere

I've discussed at great lengths many aspects of Azure Cloud Shell. Some of my recent posts include : 

* [Access Cloud Shell from within Microsoft Docs](http://www.michaelcrump.net/azure-tips-and-tricks11/)
* [Demystifying storage in Cloud Shell](http://www.michaelcrump.net/azure-tips-and-tricks13/)
* [Generate SSH public key to log into Linux VM with Cloud Shell](http://www.michaelcrump.net/azure-tips-and-tricks14/)
* [Underlying Software in Azure Cloud Shell](http://www.michaelcrump.net/azure-tips-and-tricks15/)
* [Use PowerShell with Azure Cloud Shell](http://www.michaelcrump.net/azure-tips-and-tricks17/)

Today, I'd like to discuss the new functionality with Azure Cloud Shell, which allows you to spin up a shell in your browser by simply going to [shell.azure.com](http://shell.azure.com). 

<img style="border:3px solid #021a40" src="/files/cloudshellbrowser1.png">

Keep in mind that this is the same Cloud Shell you know and love, it is just easily accessible anywhere you have a browser. 

## Jump to the PowerShell or BASH instance

You can also specify which instance of Cloud Shell you wish to launch (ex. PowerShell or BASH) by modifying the URL.

* [shell.azure.com/powershell](https://shell.azure.com/powershell) which will launch a PowerShell instance
* [shell.azure.com/bash](https://shell.azure.com/bash) which will launch a BASH instance

## Embed Cloud Shell

According to the [docs](https://docs.microsoft.com/en-us/azure/cloud-shell/embed-cloud-shell), you can easily embed this into Markdown or a Pop-up. 

For instance, this button [![Launch Cloud Shell](https://shell.azure.com/images/launchcloudshell.png "Launch Cloud Shell")](https://shell.azure.com) was created using the Markdown the docs team provided. They also have a sample for a pop-up. 

Very cool!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 