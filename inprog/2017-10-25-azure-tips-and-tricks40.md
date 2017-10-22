---
layout: post
title: "Azure Tips and Tricks Part 40 - Upload Files from a URL with Azure Logic Apps"
excerpt: "Learn how to upload files from a URL with Azure Logic Apps"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--primary} 

## My Scenario - Tracking Run Data

I thought I'd use this week's Tip and Tricks series to show a practical example of how I am using Azure. I've started running outdoors and would like to extract several links that my app generates via email and send them to my OneDrive account automatically vs doing it manually after each run. I'm also concerned that the app that generates my data may be abandoned one day. In order to secure my data, I used a combination of [Zappier.com](http://www.zapier.com) and [Azure](http://www.azure.com) to solve my problem and over the course of this week, we'll cover the following sections needed in order to implement this: 

* [Parse Emails to be used in a Azure Logic Apps](http://www.michaelcrump.net/azure-tips-and-tricks37/)
* [Create JSON Schema to be used in a Azure Logic Apps](http://www.michaelcrump.net/azure-tips-and-tricks38/)
* [Setup an HTTP Request Trigger that is used in an Azure Logic Apps](http://www.michaelcrump.net/azure-tips-and-tricks39/)
* [This post - Upload Files from a URL with Azure Logic Apps](http://www.michaelcrump.net/azure-tips-and-tricks40/)


## Upload Files from a URL with Azure Logic Apps

In the [last post](http://www.michaelcrump.net/azure-tips-and-tricks39/), we setup our Azure Logic App to receive an HTTP Request from Zappier which included a JSON payload with the four fields that we wish to extract from our email. (filename, csv, gpx and kml url)

We'll pick up by working with our existing Azure Logic App and using OneDrive to automatically upload the files to my personal OneDrive account. 

<img style="border:3px solid #021a40" src="/files/onedriveblog1.png">

Typically, you'll add an **Action** or **Condition** to trigger once the HTTP request is complete. 

We'll select an **Action** as we want it to run every time vs. an **Condition** which would use "If..then.." logic after the HTTP request comes in. Select **Action** and search for "upload file to onedrive" and you'll see the following is available to use. 

<img style="border:3px solid #021a40" src="/files/onedriveblog2.png">

You'll have to sign in to your OneDrive account. 

Now you can pull the fields that we captured and use them as dynamic content. For example, the GPX file contains the full URL, so we can just use that dynamic field. For the destination URL, we'll construct where we want it to go in our OneDrive account. Note that I've also setup 2 additional OneDrive actions for the KML and CSV file. 

<img style="border:3px solid #021a40" src="/files/onedriveblog3.png">

Now you'd want to send an email to your Zappier mailbox to test all the pieces to this app. If everything goes well, then you can switch over to your OneDrive account and you'll see your new files. 

<img style="border:3px solid #021a40" src="/files/onedriveblog4.png">

If it doesn't appear to be working then you should start by looking at the **Overview** section, then the **Run History** as shown below. 

<img style="border:3px solid #021a40" src="/files/onedriveblog5.png">

I'm really amazed by using Azure Logic Apps. I was able to create the app in less time than it took to write this up! I've barely scratched the surface with what you can do with Azure Logic Apps, but hope this gives you a good idea.  

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 