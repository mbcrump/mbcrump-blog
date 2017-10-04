---
layout: post
title: "Azure Tips and Tricks Part 27 - Configure a Backup for you Azure App Service and Database"
excerpt: "Learn how to configure a Backup for you Azure App Service and Database"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Configure a Backup for you Azure App Service and Database

Most folks don't realize how easy it is to configure a backup copy of your Azure App Service to ensure you have restorable archive copies of your app and database. In order to take advantage of this, you'll need to log into your Azure account and go to your App Service that you created and look under **Settings** then you will see **Backup**. 

<img style="border:3px solid #021a40" src="/files/backupazure1.png">

Open it and select **Configure** and you'll see the following screen. 

<img style="border:3px solid #021a40" src="/files/backupazure2.png">

You'll want to configure the **Backup Storage** first as that sets the container that you'll use to store your backup. 

<img style="border:3px solid #021a40" src="/files/backupazure3.png">

I simply gave it a name, used stardard performance and setup replication and location. 

Now you'll need to configure a container to store your backup. 

<img style="border:3px solid #021a40" src="/files/backupazure4.png">

Next, you'll want to make sure that **Scheduled backup** is set to **On**. You'll want to configure the Days and Hours and then the current schedule that it should backup from. I set mine to backup every **7** days and starting from now. You'll also want to set the retention and by default it will keep as least one backup. If you have a database, then you can also add it with just a checkmark. 

Once everything is set, you can see whatn the next backup is configured and can either force it manually or restore from an existing backup with just a visit to the Azure Portal. 

<img style="border:3px solid #021a40" src="/files/backupazure5.png">

Once it completed, you can click on the backup and see a feature called **Snapshot** which automatically create periodic restore points of your app when hosted in a Premium App Service plan. You can even download a zip of the app. 

<img style="border:3px solid #021a40" src="/files/backupazure6.png">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--inverse} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 