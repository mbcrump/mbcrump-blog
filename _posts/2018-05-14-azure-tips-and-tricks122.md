---
layout: post
title: "Azure Tips and Tricks Part 122 - Creating an IoT Hub for the IoT Button"
excerpt: "Learn how to configure and explore working with the IoT Button"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## The Series So Far

At Build 2018, we first saw the [IoT Button](http://aka.ms/button). I started [exploring the device](https://www.youtube.com/watch?v=OdGHWwRBf_c) with the very first unboxing and decided to create a mini-series to walk you how to use the device from start to finish. The series (so far) is located below

* [This post - Creating an IoT for the IoT Button](http://www.michaelcrump.net/azure-tips-and-tricks122/)
* [Configuring and Setting up the IoT Button](http://www.michaelcrump.net/azure-tips-and-tricks123/)
* [Creating the Azure Logic App for our IoT Button](http://www.michaelcrump.net/azure-tips-and-tricks124/)
* Creating the Azure Function to tie it all together

I recently recorded a fun video with my daughter unboxing the new [IoT Button](http://aka.ms/button) that was handed out at Build 2018. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/OdGHWwRBf_c?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## We need an IoT Hub, Captain!

Before we can start enjoying the IoT Button, we first need to setup an IoT Hub. 

Go inside of the Azure Portal and search for **IoT Hub** and begin to create one. Fill out the following information, but keep notepad open and save the **IoT Hub Name**. 

<img style="border:3px solid #021a40" src="/files/iotbutton1.png">

Make sure that you select the **Free Tier** and you can leave the rest at defaults. If you already have an IoT Hub with a free tier, then you'll need to either use that one or delete it to create another free tier. 

<img style="border:3px solid #021a40" src="/files/iotbutton2.png">

Once it creates, save your Hostname as you'll use that later. 

<img style="border:3px solid #021a40" src="/files/iotbutton3.png">

You'll want to click on **Shared Access Policies** and then **iothubowner** and copy and paste the **Conneection String - Primary** for later use.

<img style="border:3px solid #021a40" src="/files/iotbutton4.png">

Now download [Device Explorer](https://github.com/Azure/azure-iot-sdks/releases) for Windows or you can use the iothub-explorer tool for Mac. Now paste in your IoT Hub Connection string and press **Update**. You should see SAS populate. 

<img style="border:3px solid #021a40" src="/files/iotbutton5.png">

Switch over to the **Management** tab and click **Create** and give it a name and select **Auto-Generate Keys**, and then **Create**.

<img style="border:3px solid #021a40" src="/files/iotbutton6.png">

The keys are now created, copy them someplace safe. 

<img style="border:3px solid #021a40" src="/files/iotbutton7.png">

Right click on the newly created device and select **Copy connection string for selected device**. Now that you have they keys, we'll need to configure the device tomorrow. 

<img style="border:3px solid #021a40" src="/files/iotbutton8.png">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 