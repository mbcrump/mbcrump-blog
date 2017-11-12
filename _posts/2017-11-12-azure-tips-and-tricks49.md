---
layout: post
title: "Azure Tips and Tricks Part 49 - Add Azure Cloud Shell to Visual Studio Code"
excerpt: "Learn how to add Azure Cloud Shell to Visual Studio Code"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Add Azure Cloud Shell to Visual Studio Code

I'm a big fan of [Visual Studio Code](http://twitter.com/code) and [Azure Cloud Shell](https://azure.microsoft.com/en-us/features/cloud-shell/) and recently saw this [tweet](https://twitter.com/fiveisprime/status/928774771763900416) by Matt Hernandez and had to add it to this Azure Tips and Trick list. If you've been following the series, then you'd know that I covered Azure Cloud Shell and MS Docs back in [post 11](https://www.michaelcrump.net/azure-tips-and-tricks11/) and how to use PowerShell in Azure Cloud Shell in [post 17](https://www.michaelcrump.net/azure-tips-and-tricks17/). Today, we'll cover how to add Azure Cloud Shell to Visual Studio Code. 

It is fairly easy as all you need to do is open VS Code, click on Extensions and search for `azure account` and install it as shown below. 

<img style="border:3px solid #021a40" src="/files/azurevscode1.png">

Once installed, go to View -> Command Palette and type `Open Bash in Cloud Shell`. 

<img style="border:3px solid #021a40" src="/files/azurevscode2.png">

**Note:** You can also open PowerShell in Cloud Shell with this extension!
{: .notice--primary}

You'll need to sign in first and VS Code makes that simple by opening the browser and copying your device authentication code. Once that is complete, you'll see: 

<img style="border:3px solid #021a40" src="/files/azurevscode3.png">

Go back to View -> Command Palette and select `Open Bash in Cloud Shell` again and it should spin up as shown below.

 <img style="border:3px solid #021a40" src="/files/azurevscode4.png">

 Very cool and if you want to see the source code for the app, then it can be found [here](https://github.com/Microsoft/vscode-azure-account).

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 