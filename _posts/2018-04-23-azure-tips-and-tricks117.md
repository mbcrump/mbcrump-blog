---
layout: post
title: "Azure Tips and Tricks Part 117 - Enable HTTP 2.0 support for Azure App Service"
excerpt: "A tutorial on how to enable HTTP/2.0 support for Azure App Service"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Tips and Tricks Videos are NOW Available!** : Get all the goodness of Azure Tips and Tricks in video form. [Read more about it here](http://www.michaelcrump.net/azure-tips-and-tricks106/)
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Enable HTTP/2.0 support for Azure App Service

Azure has recently rolled out the ability for you to switch any app service to use HTTP/2.0 Support. It really is as easy as toggling a field in Azure Resource Manager, but first why should you care about HTTP/2.0?

HTTP/2 supports queries multiplexing, headers compression, priority and more intelligent packet streaming management. All of this results in reduced latency and accelerates content download on modern web pages which you should be writing now. :) If you want more details, then [this source](https://daniel.haxx.se/http2/) is the one that I personally trust. 

## Getting Started

Before you go to the Azure Portal, take your *.azurewebsites.net url and test it [here](https://tools.keycdn.com/http2-test). It will quickly tell you whether or not your site supports HTTP/2.0. The reason that I want to start with this site is because in the future HTTP/2.0 will be automatically enabled on future *.azurewebsites.net urls.

Switch over to the **Azure Portal** now and click on **App Service** and then your existing site. Now click on **Resource Explorer** as shown below. 

<img style="border:3px solid #021a40" src="/files/azhttp2-1.png">

It should navigate you to Azure Resource Explorer (Preview) and you'll just need to click on **config** and then **web**. 

<img style="border:3px solid #021a40" src="/files/azhttp2-2.png">

Click on Read/Write, then toggle `"http20Enabled": false` to `"http20Enabled": true` and click **Put**. 

<img style="border:3px solid #021a40" src="/files/azhttp2-3.gif">

Now you can go back to our [HTTP/2.0 testing tool](https://daniel.haxx.se/http2/) and input your *.azurewebsites.net url. I tested mine and received the following: 

<img style="border:3px solid #021a40" src="/files/azhttp2-4.png">

Looks like I'm set! Happy coding!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 