---
layout: post
title: "Azure Tips and Tricks Part 131 - Quickly display a list of all Azure Web Apps URL from Azure Cloud Shell"
excerpt: "Learn how to quickly display a list of all Azure Web Apps URL from Azure Cloud Shell"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Check out Azure.Source by [Rob Caron](https://twitter.com/RobCaronMSFT)** : A very nice mix of Azure news, announcements, videos, podcast and more. [Read weekly](https://azure.microsoft.com/en-us/blog/azure-source-volume-35/)
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Quickly display a list of all Azure Web Apps URL from Azure Cloud Shell

Often I need to quickly list out the URLs for all Azure App Services in a given resource. In the past, when it just a small number then I'd do it manually, but it has recently grown to a point where I needed to find a better way. 

Enter PowerShell and Azure Cloud Shell. 

Wherever you are logged in with Azure Cloud Shell and are using PowerShell, then you can quickly run this command:

`Get-AzureRmWebApp | foreach-object {$_} | select-object SiteName, DefaultHostName, ResourceGroup`

<img style="border:3px solid #021a40" src="/files/powershellallwebsites.png">

It will give you the domain name, the *.azurewebsites.net and the resource group that it is contained in. Simple!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 