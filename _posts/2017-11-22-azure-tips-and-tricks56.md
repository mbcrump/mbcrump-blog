---
layout: post
title: "Azure Tips and Tricks Part 56 - Deploy a .NET Core WebAPI Project to Web App for Containers"
excerpt: "Learn how to use deploy a .NET Core WebAPI Project to Azure"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use .NET Core WebAPI and Docker Compose

How hard do you think it is to:

* [Create and Publish a .NET Core WebAPI project](http://www.michaelcrump.net/azure-tips-and-tricks54/)
* [Add it to a Docker Container using Docker Compose and push it to a Docker Cloud](http://www.michaelcrump.net/azure-tips-and-tricks55/)
* [Today - Use it in Azure with Web App for Containers](http://www.michaelcrump.net/azure-tips-and-tricks56/)

In this mini-series, we'll build on each part starting with creating and publishing a .NET Core WebAPI project. Yesterday, we used Docker Compose to create an image and push it to Docker Cloud and we'll wrap up today by deploying it to Azure using [Web App for Containers](https://azure.microsoft.com/en-us/services/app-service/containers/). 

## Deploy a .NET Core WebAPI Project to Web App for Containers

Remember [yesterday](http://www.michaelcrump.net/azure-tips-and-tricks55/), how we pushed our Docker Image to Docker Cloud? As a reminder, we created a repository in Docker Cloud and headed back to our command prompt (or terminal) and ran the following commands: 

`docker login` to authenticate 

`docker push mbcrump/mbcwebapi:latest` to push your image to Docker Cloud. 

Now that we have a Docker Cloud repository, we can push it to Azure using [Web App for Containers](https://azure.microsoft.com/en-us/services/app-service/containers/). 

Go ahead and log into the Azure Portal and search for `Web App for Containers`. You should see the following: 

<img style="border:3px solid #021a40" src="/files/webappcont1.png">

Press the `Create` button and you should see the following: 

<img style="border:3px solid #021a40" src="/files/webappcont2.png">

You should be familiar with (name, resource group, etc.) with the exception being the `Configure Container` section. 

Here we will use Docker Hub (think Docker Cloud), our repo is public, and the name of the image. Which follows the format `docker username/our app name:tag`. For a refresher, visit [Step 2 in yesterday's post](https://www.michaelcrump.net/azure-tips-and-tricks55/). 

After our Web App for Container is deployed, you can simply go to your new url and append `/api/values` to see your new site. 

<img style="border:3px solid #021a40" src="/files/webappcont3.png">

That's it. You now have a WebAPI running inside a Docker Container hosted on Azure with a public site which you can call from. That was too easy!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 