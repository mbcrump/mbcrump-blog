---
layout: post
title: "Azure Tips and Tricks Part 64 - Using a different route prefix with Azure Functions"
excerpt: "Learn how to use a different route prefix with Azure Function"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Using a different route prefix with Azure Functions

Sometimes you have the requirement to use a different route prefix than the one that Azure Functions auto-generates

For example: `https://mynewapimc.azurewebsites.net/api/HttpTriggerCSharp1` uses `api` before the function name. You might want to either remove `api` or change it to another name. 

I typically fix this by going into the Azure Portal and clicking on my Azure Function. I then click on **Platform Features** and **Advanced tools(Kudu)**. 

<img style="border:3px solid #021a40" src="/files/azfunckudu1.png">

I then navigate to `wwwroot` and hit edit on the `host.json` file. 

<img style="border:3px solid #021a40" src="/files/azfunckudu2.png">

Inside the editor, add the `routePrefix` to define the route prefix. So if I wanted the route prefix to be blank, then I'd `use the following:

```json
{
  "http": {
    "routePrefix": ""
  }
}
```

Simply restart your Azure Function and now my URL is accessable without `api`.

<img style="border:3px solid #021a40" src="/files/azfunckudu3.png">

On the flip side, if you wanted a route prefix, then I'd just add the following

```json
{
  "http": {
    "routePrefix": "myroute"
  }
}
```

<img style="border:3px solid #021a40" src="/files/azfunckudu4.png">

Keep in mind that best practice (as far as I can tell) is to use `api`, but wanted to flag this as only you can make your design decisions. 
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 