---
layout: post
title: "Azure Tips and Tricks Part 134 - Use Run-From-Zip to deploy a site to Azure Web Apps or Functions"
excerpt: "Learn how to use Run-From-Zip to deploy a site to Azure Web Apps or Functions"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use Run-From-Zip to deploy a site to Azure Web Apps or Functions

Here is a neat feature that I just discovered dispite it being added about 6 months or so ago. It is the ability to deploy a site to Azure Web Apps or Azure Functions from a zip file. 

With **Run-From-Zip** there is no longer a deployment step which copies the files to wwwroot such as git, ftp, etc. Instead, the zip file that you point to in your App Settings gets mounted on wwwroot as read-only. 

To get started: 

Using **Azure Storage Explorer**, create a storage blob container and upload your zip file and select **Generate SAS Signature** as shown below:

<img style="border:3px solid #021a40" src="/files/azblobfunction1.png">

Hit **Create** and then **Copy**

<img style="border:3px solid #021a40" src="/files/azblobfunction2.png">

<img style="border:3px solid #021a40" src="/files/azblobfunction3.png">

Now head back over to the Azure Portal and add an Azure App Setting called `WEBSITE_RUN_FROM_ZIP`, and point it to your zip file. 

Mine looks like : `WEBSITE_RUN_FROM_ZIP=https://REMOVED.blob.core.windows.net/michael-test/MichaelSampleApp.zip?st=2018-06-24T22%3A16%3A40Z&se=2018-06-25T22%3A16%3A40Z&sp=rl&sv=2017-07-29&sr=b&sig=01h%3D`

Now gives your site a couple of seconds and you should see your site that was deployed via a zip file. 

That is it! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 