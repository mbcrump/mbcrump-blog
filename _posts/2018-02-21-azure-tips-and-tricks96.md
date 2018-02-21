---
layout: post
title: "Azure Tips and Tricks Part 96 - Getting up and started with Azure IoT MXChip"
excerpt: "Learn how to get up and running with Azure IoT MXChip"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Getting up and running with Azure IoT MXChip

I recently was given an Azure IoT DevKit that included the new [MXChip](http://mxchip.com/az3166). The chip is very impressive and while it supports a lot of amazing features, the following caught my eyes:

* OLED,128×64
* 2 user button
* Motion sensor
* Magnetometer sensor
* Atmospheric pressure sensor
* Temperature and humidity sensor

On first boot, it wanted me to configure my Wifi. Since it automatically creates an AP, I was able to use my iPhone to connect to the MXChip's AP and enter my home network for it to connect to. 

<img style="border:3px solid #021a40" src="/files/iotdevkit1.png">

<img style="border:3px solid #021a40" src="/files/iotdevkit2.png">

<img style="border:3px solid #021a40" src="/files/iotdevkit3.png">

Great! It now reboots and I'm on my home WiFi. 

**Note** It can only store one WiFi profile, so if you take it into your office and bring it back home then you'll be configuring it a lot. 
{: .btn .btn--success} 

Next up was noticing that my firmware needed to be upgraded. Thankfully this is as simply as [navigating to this page](https://microsoft.github.io/azure-iot-developer-kit/docs/firmware-upgrading/) and placing the files on the root of the MXChip once you plug it into your USB port. 

<img style="border:3px solid #021a40" src="/files/iotdevkit4.png">

<img style="border:3px solid #021a40" src="/files/iotdevkit5.png">

Now you probably want to test your device by pressing the **B** button. This cycles through various features of the device as shown below. 

<img style="border:3px solid #021a40" src="/files/iotdevkit6.png">

<img style="border:3px solid #021a40" src="/files/iotdevkit7.png">

Now all that is left to do is to download a script that installs all necessary files along with VS Code. If you already have some of them installed, the script will can and skip them.

Get it here for [Windows](https://aka.ms/devkit/prod/installpackage/latest) or [Mac](https://aka.ms/devkit/prod/installpackage/mac/latest)

It contains the following: 

* Node.js and Yarn: Runtime for the setup script and automated tasks.
* Azure CLI 2.0 MSI - Cross-platform command-line experience for managing Azure resources. The MSI contains dependent Python and pip.
* Visual Studio Code (VS Code): Lightweight code editor for DevKit development.
* Visual Studio Code extension for Arduino: Extension that enables Arduino development in Visual Studio Code.
* Arduino IDE: The extension for Arduino relies on this tool.
* DevKit Board Package: Tool chains, libraries, and projects for the DevKit
* ST-Link Utility: Essential tools and drivers.

That's it. Now you can begin working with a project [here](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/). 

Happy Coding!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 