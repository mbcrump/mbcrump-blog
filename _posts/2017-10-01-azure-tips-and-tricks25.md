---
layout: post
title: "Azure Tips and Tricks Part 25 - Use the Azure Resource Explorer to quickly explore REST APIs"
excerpt: "Learn how to use the Azure Resource Explorer to quickly explore REST APIs"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Intro

We've recently created a [web app](http://www.michaelcrump.net/azure-tips-and-tricks19/) and uploaded it to Azure App Service. We also took a look at [multiple ways](http://www.michaelcrump.net/azure-tips-and-tricks20/) to examine those files through the Azure portal interface and how we'd add [extensions](http://www.michaelcrump.net/azure-tips-and-tricks21/) and [deployment slots](http://www.michaelcrump.net/azure-tips-and-tricks22/) for our web app. We also took a look at a feature called [Testing in Production](http://www.michaelcrump.net/azure-tips-and-tricks23/) which allows us to distribute traffic between our production and other slots. We also looked at using [PowerShell](http://www.michaelcrump.net/azure-tips-and-tricks24/) to automatically distribute the load between your Production and deployment slot sites with the Testing in Production feature. In this post, we'll continue exploring our web app with a feature called Azure Resource Explorer which will allow us to quickly explore REST APIs.  

## Use the Azure Resource Explorer to quickly explore REST APIs

The Azure Resource Manager allows you to explore (and learn) REST APIs in your Azure Subscription in a friendly fashion. If you log into your Azure account and go to your App Service that you created and look under **Development Tools** then you will see it. 

<img style="border:3px solid #021a40" src="/files/azureresourceexplorer1.png">

Inside the blade, it will redirect you to [https://resources.azure.com](https://resources.azure.com) and you'll see your current app. You can also go back to the url without entering the portal, but will have to manually browse to your app.

<img style="border:3px solid #021a40" src="/files/azureresourceexplorer2.png">

There is a navigation tree that you can click on to drill into the current web app. As you click the URL and JSON returned will update. You'll also notice that there is an **Edit** button that you can use to call a PUT to update an item as shown below. 

<img style="border:3px solid #021a40" src="/files/azureresourceexplorer3.gif">

**Note:** Keep in mind that you'll need to be in `Read\Write` mode to do this which can be found in the top panel by your name. 
{: .notice--info}

You can also perform a POST or DELETE on some resources as well as Create. There is documentation, but what is very interesting to me is the **PowerShell** and **CLI 2.0** options. If you click on **CLI 2.0** for a resource then you'll see the following. 

<img style="border:3px solid #021a40" src="/files/azureresourceexplorer4.png">

Awesome! That is the CLI 2.0 commands we could use in BASH or wherever the CLI 2.0 is supported. 

If we were looking in the following node of our web app and say for example that we want to update the `logsDirectorySizeLimit` property, then we could start taking advantage of this feature. 

<img style="border:3px solid #021a40" src="/files/azureresourceexplorer5.png">

In this example, I clicked on the `CLI 2.0` link and it provided the following code: 

```bash
az resource show --id /subscriptions/d1ecc7ac-c1d8-40dc-97d6-2507597e7404/resourceGroups/StaticResourceGroup/providers/Microsoft.Web/sites/MyQuizApplication/config/web --api-version 2016-08-01

az resource update --id /subscriptions/d1ecc7ac-c1d8-40dc-97d6-2507597e7404/resourceGroups/StaticResourceGroup/providers/Microsoft.Web/sites/MyQuizApplication/config/web --api-version 2016-08-01 --set properties.key=value
```

The only value that we'd need to update is on the last line with the `--set properties.key=value`. Since we want to just update the `logsDirectorySizeLimit` property then we can do so with `--set properties.logsDirectorySizeLimit=40`. 

The complete command is shown below. 

```bash
az resource show --id /subscriptions/d1ecc7ac-c1d8-40dc-97d6-2507597e7404/resourceGroups/StaticResourceGroup/providers/Microsoft.Web/sites/MyQuizApplication/config/web --api-version 2016-08-01

az resource update --id /subscriptions/d1ecc7ac-c1d8-40dc-97d6-2507597e7404/resourceGroups/StaticResourceGroup/providers/Microsoft.Web/sites/MyQuizApplication/config/web --api-version 2016-08-01 --set properties.logsDirectorySizeLimit=40
```
I could now switch back over to my browser and press the **GET** button to see that the `logsDirectorySizeLimit` has now been updated to 40. 

<img style="border:3px solid #021a40" src="/files/azureresourceexplorer7.png">


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--inverse} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 