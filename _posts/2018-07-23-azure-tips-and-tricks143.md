---
layout: post
title: "Azure Tips and Tricks Part 143 - Keep your Azure Web App Hydrated and Responsive"
excerpt: "Learn how to easily keep your Azure Web App hydrated and responsive"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Keep your Azure Web App Hydrated and Responsive

If you have ever noticed that after a publish or restart of your Azure web app it might load slowly the first time, then when you refresh with F5 it is ok again. 

If you've ever noticed this behavior an option **might** be to go inside of the **Application Settings** for the web app in the portal, and activating **Always On**, which keeps your web hydrated and responsive.

<img style="border:3px solid #021a40" src="/files/azurewebappalwayson1.png">

According to the information icon: 

> Indicates that your web app needs to be loaded at all times. By default, web apps are unloaded after they have been idle. It is recommended that you enable this option when you have continuous web jobs running on the web app.

Keep in mind that you will not be able to turn this feature on when using the **Free version** of Azure App Services. It is only available in **Basic** or **Standard** plans.

To recap, if your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.

It is worth giving a shot if you encounter these issues. Until next time, Michael signing off!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 