---
layout: post
title: "Azure Tips and Tricks Part 43 - Working with Azure Logic App using Visual Studio 2017"
excerpt: "Learn how to use Visual Studio 2017 to work with Azure Logic App"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Working with Azure Logic App using Visual Studio 2017

A great tip that I remember learning from [Jeff Hollan](https://twitter.com/jeffhollan?lang=en) is that folks can work with Logic Apps with Visual Studio. I'm going to use Visual Studio 2017 but previous version work as well. 

Fire up Visual Studio 2017 and select **File** -> **New Project** -> **Cloud** -> **Resource Group**

<img style="border:3px solid #021a40" src="/files/vs2017logicapp1.png">

Give it a name and then you'll need to choose a template. Scroll down until you see **Logic App**. 

<img style="border:3px solid #021a40" src="/files/vs2017logicapp2.png">

Once everything spins up, you'll notice you have the following file structure in Visual Studio. 

<img style="border:3px solid #021a40" src="/files/vs2017logicapp3.png">

* Deploy-AzureResourceGroup.ps1 - Is a PowerShell deployment script for the Logic App
* LogicApp.json - This is where your main logic for your Logic App Lives
* LogicApp.parameters.json - The parameters file that you'll mostly want to leave alone

If you click on the **LogicApp.json** you'll see the code and a **JSON Outline** in Visual Studio and you could begin hand coding your app, but I'd rather use a designer. Go ahead and go to **Tools** and **Extensions** and search for **Logic Apps** and press **Download**. 

<img style="border:3px solid #021a40" src="/files/vs2017logicapp4.png">

A VSIX installer will appear after you close out of Visual Studio and just follow the steps to install it. 

<img style="border:3px solid #021a40" src="/files/vs2017logicapp5.png">

Now you can right click your **LogicApp.json** and have the ability to open it with the Designer! 

<img style="border:3px solid #021a40" src="/files/vs2017logicapp6.png">

You'll need an internet connection and it will prompt you to log in. 

<img style="border:3px solid #021a40" src="/files/vs2017logicapp7.png">

Bingo! Now you're cooking with Fire! You can work with the designer just like you did in the Azure Portal. 

<img style="border:3px solid #021a40" src="/files/vs2017logicapp8.png">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 