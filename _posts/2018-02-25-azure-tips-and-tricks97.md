---
layout: post
title: "Azure Tips and Tricks Part 97 - Generate a Weekly Digest Email for a Blog using Azure Functions, SendGrid and Azure Storage"
excerpt: "Learn how to generate a weekly digest email for a blog using Azure Functions, SendGrid and Azure Storage"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Developer Guide Book 2nd Edition available now!** This free eBook is available now at [aka.ms/azuredevebook](https://aka.ms/azuredevebook).
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## The Problem

While reading a blog post, one of these popped up: 

<img style="border:3px solid #021a40" src="/files/emailsub1.png">

We've all seen then before, and I must admit that I've never really looked into it before I started writing [this Azure Tips and Tricks series](https://michaelcrump.net/azure-tips-and-tricks-complete-list/). 

We're all crazy busy, so it seems to be a good idea, for someone to give you an email address and be notified of new posts. OK, so I wanted to do it, and started looking into sites that offer this. After looking around, I kept finding this:

<img style="border:3px solid #021a40" src="/files/emailsub2.png">

Most companies offer you a certain number of subscribers for free, then you'll quickly get to a paid version once you go over that number. 

Since I like to save a penny now and again and am aware that I have more subscribers that the free account offers (200), I decided to roll my own. But what would I need? 

## My Requirements to roll my own

My requirements for my version of creating an email subscription is the following: 

* A way to email folks for free or really, really cheap.
* Storage to save the email address and a way to indicate if they want to unsubscribe.
* A web page that folks can fill out that can make a POST call.
* Code running in the cloud (1) on a schedule and (2) perform actions based on a POST request.
* Visual Studio and C# as I'm well versed in them.

## My Stack

After poking around for a bit, I landed on the following:

* SendGrid will handle email (25K emails free monthly)
* Azure Storage Tables to save the email address and subscription status (this gives me an unlimited number of subscribers). 
* Timer Trigger with Azure Functions to run on a schedule to send emails. (Runs weekly and retrieves my last 7 days worth of blog posts)
* HTTP Trigger with Azure Functions to collect POST data coming from my website that contains the email address and subscription status that someone types in. 
* Azure Functions supports Visual Studio tooling and the full .NET Framework. (in case, I want to use something outside of .NET Core)

## Creating a SendGrid account

Go to the **Azure Portal** and search services for **SendGrid** and create an account as shown below. You'll notice that I used the **Free** account as it is good enough for what I was trying to accomplish. 

<img style="border:3px solid #021a40" src="/files/sendgrid1.png">

Go to your SendGrid account once provisioned and click on **Manage** and it will bring you to [https://app.sendgrid.com/](https://app.sendgrid.com/). From the SendGrid portal, you are going to want to grab your API key. You can find it under **Settings**, then **API Keys**. Give your API Key a name and then give it **Full Access** and click **Create and View**. Now that you have your API Key, save it somewhere safe.

## Creating an Azure Storage Table

Go back to the Azure Portal and click **Create a Resource** and select **Azure Storage**. We'll keep it simple as shown below to get started. 

<img style="border:3px solid #021a40" src="/files/storageacct1.png">

Once complete, go into the resource and look under **Services**. 

<img style="border:3px solid #021a40" src="/files/storageacct2.png">

Go ahead and click on **Tables** and you could create a new table through the portal as shown below.

<img style="border:3px solid #021a40" src="/files/aztablesblog1.png">

Go ahead and give the table a name that you'll remember and look under **Settings**, then **Access Keys** and copy the connection string as we'll use that shortly. 

<img style="border:3px solid #021a40" src="/files/storagethroughcsharp1.png">

Now that we have our **SendGrid** account and our **Azure Storage Table** created. We can proceed. 

## Open Visual Studio

Create a C# Azure Function application by opening Visual Studio and selecting the template under the **Cloud** node as shown below:

<img style="border:3px solid #021a40" src="/files/emailsub3.png">

Under Storage, change the default emulator to the **Azure Storage Account** that we created earlier:

<img style="border:3px solid #021a40" src="/files/emailsub4.png">

We'll begin by using the **Timer Trigger** and leaving everything as the defaults. 

<img style="border:3px solid #021a40" src="/files/emailsub5.png">

Once the project spins up, we'll use NuGet to pull in references to :

* WindowsAzure.Storage `To work with Azure Table Storage.`
* Microsoft.WindowsAzure.ConfigurationManager `To hide our API keys`
* Sendgrid `To send our emails`
* System.ServiceModel.Syndication `To work with RSS feeds - use prerelease packages to find it`

Looking good so far and a good stopping point for today. Come back soon for the next post in the series where we'll begin putting this all together. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 