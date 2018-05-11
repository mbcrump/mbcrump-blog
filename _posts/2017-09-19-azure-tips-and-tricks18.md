---
layout: post
title: "Azure Tips and Tricks Part 18 - Use Tags to quickly organize Azure Resources"
excerpt: "Learn how to take advantage of tags to organize your Azure resources"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List

[Click here to view the complete list of Azure Tips and Tricks ](https://michaelcrump.net/azure-tips-and-tricks-complete-list/)

## Video Available

<iframe width="560" height="315" src="https://www.youtube.com/embed/Ho_zV3jh0xg?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Use Tags to quickly organize Azure Resources

If you've ever wanted to quickly organize Azure Resources then you can utilize tags to do so. For example, if you'd like to have a set of Resources for "Production" and another for "Dev", then you can quickly do that. 

Head over to the Azure Portal and select service. In my example, I'm going to select a Web App that I want to tag as a production app. Select the **Tags** menu and provide a Name and Value as shown below.  

<img style="border:3px solid #021a40" src="/files/azuretag1.png">

**Remember this!** Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.
{: .notice--primary}

I selected "Environment" and gave it the value of "Production". I then clicked "Save". I could also do this for other Production resources and even tag the appropriate ones with "Dev".

I can now take advantage of this by going to **More Services** and typing **Tags** and click on the Environment: Production as shown below. 

<img style="border:3px solid #021a40" src="/files/azuretag2.png">

1. Results from searching "Tags"
2. Our Production Environment we just setup
3. List all the Web Apps with the Production Environment Tag
4. Pin the Blade to our Azure Portal Main Page

If you pin the blade (by pressing the pin in step 4.), then you'll see the following on your Azure Portal dashboard

<img style="border:3px solid #021a40" src="/files/azuretag3.png">

You can even interact with **Tags** using Azure CLI 2.0. For example, I can type `az tag list -o json` to list all the tags associated with an account.

``` shell
michael@Azure:~$ az tag list
[
  {
    "count": {
      "type": "Total",
      "value": 2
    },
    "id": "/subscriptions/c0e5fb0f-7461-4b04-9720-63fe407b1bdb/tagNames/Environment",
    "tagName": "Environment",
    "values": [
      {
        "count": {
          "type": "Total",
          "value": 1
        },
        "id": "/subscriptions/c0e5fb0f-7461-4b04-9720-63fe407b1bdb/tagNames/Environment/tagValues/Dev",
        "tagValue": "Dev"
      },
      {
        "count": {
          "type": "Total",
          "value": 1
        },
        "id": "/subscriptions/c0e5fb0f-7461-4b04-9720-63fe407b1bdb/tagNames/Environment/tagValues/Production",
        "tagValue": "Production"
      }
    ]
  }
]
```

There is a lot more use cases for using Tags, but this is the one that I use it most frequently for. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 