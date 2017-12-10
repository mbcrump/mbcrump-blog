---
layout: post
title: "Azure Tips and Tricks Part 65 - Use Visual Studio Code to work with Cosmos DB"
excerpt: "Learn how to use Visual Studio Code to work with Cosmos DB"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use Visual Studio Code to work with Cosmos DB

**What is Cosmos DB?** Azure Cosmos DB is Microsoft's globally distributed, multi-model database. For more info visit [this page](https://docs.microsoft.com/en-us/azure/cosmos-db/introduction).
{: .notice--primary}

Something that I wasn't aware of until yesterday is the [Visual Studio Code extension for Azure Cosmos DB](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb).

<img style="border:3px solid #021a40" src="/files/cosmosvscode1.png">

You can easily view, create and delete databases, collections, graphs, and documents, along with other things detailed in their marketplace submission.  

After installing it via the extension above, here is what it looks like to setup our Cosmos DB resource and type from within Visual Studio Code. 

<img style="border:3px solid #021a40" src="/files/cosmosvscode2.gif">

Now we'll setup our database and collection. 

<img style="border:3px solid #021a40" src="/files/cosmosvscode2.gif">

Finally, we'll create a document and add the following data to it. 

```json
{
    "name": "learn cosmos db",
}
```

<img style="border:3px solid #021a40" src="/files/cosmosvscode3.gif">

Now we're ready to begin work! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 