---
layout: post
title: "Azure Tips and Tricks Part 63 - Open an existing Azure Function in Visual Studio"
excerpt: "Learn how to open an existing Azure Function in Visual Studio"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Open an existing Azure Function in Visual Studio

I recently wanted to modify an existing Azure Function in Visual Studio 2017 and noticed this is very straightforward. Simply log into the portal and select your Azure Function, go to **Overview** and then click on **Download app content** as shown below: 

<img style="border:3px solid #021a40" src="/files/azvsblog1.png">

You'll want to select the **Content and Visual Studio Project** as well as **Include app settings in the download**

<img style="border:3px solid #021a40" src="/files/azvsblog2.png">

**What is app settings?** This will include a `local.settings.json file which contains your application settings. 
{: .notice--primary}

Here is the content of my downloaded zip file. 

**What about third party .dlls?** Yep, they are included. 
{: .notice--primary}

<img style="border:3px solid #021a40" src="/files/azvsblog3.png">

If you open Visual Studio, you can select the folder and begin working: 

<img style="border:3px solid #021a40" src="/files/azvsblog4.png">

From here, I'd probably setup continuous deployment through pushing the code to GitHub and using the **Deployment options** found inside **Platform features** in the Azure portal. 

<img style="border:3px solid #021a40" src="/files/azvsblog5.png">

**What about C# projects?** You will get a .csproj file in the output folder along with C# scripts (csx files). 
{: .notice--primary}

As always, I hope this helps! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 