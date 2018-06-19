---
layout: post
title: "Azure Tips and Tricks Part 133 - Use the Azure Portal for Durable Functions Development"
excerpt: "Learn how to quickly use the Azure Portal for Durable Functions Development"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use the Azure Portal for Durable Functions Development

Durable Functions addresses the task of managing state for an application. They are intended to address a variety of patterns and scenarios that would quickly get complicated using triggers, timers, etc. especially when orchestrating a range of activities with a set of tasks that need to happen each time a particular event occurs.

Here is one example: I have one task, that causes another task to occur, and so on with some conditional statements and other business logic to fork the workflow but I’m trying to go from point a to point b. An example of this is called **Function chaining**. This refers to the pattern of executing a sequence of functions in a particular order.

Head over to our [docs](https://docs.microsoft.com/en-us/azure/azure-functions/durable-functions-sequence) for more info or follow along with this tutorial and it might make sense. 

### Getting Started

Log into the Azure Portal and create a new Azure Function project like the following:

<img style="border:3px solid #021a40" src="/files/azdfunc1.png">

Configure the function app to use the 2.0 runtime version in the **Function app** settings tab.

<img style="border:3px solid #021a40" src="/files/azdfunc2.png">

Create a new custom function. 

<img style="border:3px solid #021a40" src="/files/azdfunc3.png">

Search for the **Durable Functions Http Starter - C#** template.

<img style="border:3px solid #021a40" src="/files/azdfunc4.png">

Install the extention when prompted.

<img style="border:3px solid #021a40" src="/files/azdfunc5.png">

Give the orchestration client function a name **HttpStart** that is created by selecting Durable Functions Http Starter - C# template.

<img style="border:3px solid #021a40" src="/files/azdfunc6.png">

Once this is complete, then copy the URL as we'll use it later on.

Create a new orchestration function named **HelloSequence** and select **Durable Functions Orchestrator** template.

Create another function named **Hello** and use the **Durable Functions Activity** template.

Install [Postman](https://www.getpostman.com/apps), and create a POST request and use the following URL (after suppling the new Azure Function Name) : `https://yourfunctionname.azurewebsites.net/api/orchestrators/HelloSequence`

You should see the following: 

<img style="border:3px solid #021a40" src="/files/azdfunc7.png">

Click on one of the **statusQueryGetUri** URLs and you see the status of the Durable Function : 

<img style="border:3px solid #021a40" src="/files/azdfunc8.png">

Now I'd encourage you to look at the code in each Function to see how it all works together. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 