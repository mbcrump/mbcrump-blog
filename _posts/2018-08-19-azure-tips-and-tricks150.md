---
layout: post
title: "Azure Tips and Tricks Part 150 - Use the Mac Touch Bar to launch the Azure Portal"
excerpt: "Learn how to create a shortcut to Azure using the Mac Touch Bar "
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use the Mac Touch Bar to launch the Azure Portal

For those new to the Mac Touch Bar, it  sits at the top of your keyboard and adapts to what you're doing and provides intuitive shortcuts and app controls when you need them. For example, the controls will change when you are in Chrome vs Outlook. Below is a screenshot of the default layout before you switch to an application:

<img style="border:3px solid #021a40" src="/files/keyboardaz1.png">

**Screenshot courtesy of Apple**

Kinda disappointing. I felt I could do better. After searching all over I found a tool called [BetterTouchTool](https://folivora.ai/) that allows you to customize the Mac Touch Bar. After spending an entire weekend playing with it, I landed on the following layout (in case you are curious):

<img style="border:3px solid #021a40" src="/files/keyboardaz2.png">

You'll see the following from left to right:

* Shortcut to VS Code
* Shortcut to Hyper.js
* Shortcut to Azure
* Shortcut to TextEdit
* Volume
* Current Temp where I'm at
* Clipboard Manager
* Create New File in Finder with Dialog
* Copy path to current folder in Finder
* BetterTouchTool
* Brightness
* Mute
* Lock Computer
* Spotlight

Since we're interested in adding a shortcut to the Azure Portal, all you have to do is download [BetterTouchTool](https://folivora.ai/) and click on the **TouchBar** option and **Add a TouchBar Button** and configure it to open a URL such `portal.azure.com`

<img style="border:3px solid #021a40" src="/files/keyboardaz3.png">

Easy enough and will definitely get you a couple of extra nerd points!

What is also interesting is the ability to call an API and retrieve data and parse it to the Touch Bar like I did with the weather. Leave your ideas below on other ways to be more productive with Azure below. 

As always, I hoped this help someone out there! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 