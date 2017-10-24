---
layout: post
title: "Azure Tips and Tricks Part 39 - Setup an HTTP Request Trigger that is used in an Azure Logic Apps"
excerpt: "Learn how to setup an HTTP Request Trigger with Azure Logic Apps"
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
* [This post - Setup an HTTP Request Trigger that is used in an Azure Logic Apps](http://www.michaelcrump.net/azure-tips-and-tricks39/)
* [Upload Files from a URL with Azure Logic Apps](http://www.michaelcrump.net/azure-tips-and-tricks40/)


## Setup an HTTP Request Trigger that is used in an Azure Logic Apps

In the [last post](http://www.michaelcrump.net/azure-tips-and-tricks38/), we used Zappier to setup a web hook that calls a POST method that provides the filename, csv, gpx and kml url that it parsed from our email. 

We'll pick up by creating a new Azure Logic App. Go to the Azure Portal and create a new Logic App. 

<img style="border:3px solid #021a40" src="/files/logicappblog1.png">

After the resource is ready, we're are going to need to trigger an action when an HTTP request comes in. Thankfully, this is one of the **Common Triggers** and we can select it to begin. 

<img style="border:3px solid #021a40" src="/files/logicappblog2.png">

Note that the URL isn't generated until we provide the parameters. 

<img style="border:3px solid #021a40" src="/files/logicappblog3.png">

Go ahead and press **Edit** and remember the JSON Schema from the [last post](http://www.michaelcrump.net/azure-tips-and-tricks38/)? Well, now is the time to paste it in. I'll also include it below: 

```json
{
  "$schema": "http://json-schema.org/draft-06/schema#", 
  "definitions": {}, 
  "id": "http://example.com/example.json", 
  "properties": {
    "csv": {
      "id": "/properties/csv", 
      "type": "string"
    }, 
    "filename": {
      "id": "/properties/filename", 
      "type": "string"
    }, 
    "gpx": {
      "id": "/properties/gpx", 
      "type": "string"
    }, 
    "kml": {
      "id": "/properties/kml", 
      "type": "string"
    }
  }, 
  "type": "object"
}
```

**Note:** You can use the "Use sample payload to generate schema" option, but I prefer the additional meta data that [JSON Schema](https://jsonschema.net/#/editor) can provide. 
{: .notice--info}

You'll now have a GET URL that you can put in Zappier and replace the [requestb.in](https://requestb.in/) that we stubbed out earlier. 

<img style="border:3px solid #021a40" src="/files/logicappblog4.png">

Head back over to [Zappier Editor](https://zapier.com/app/editor) and modify your Zap by editing the template and replacing the requestb.in URL with your live Azure Logic Apps ones. 

<img style="border:3px solid #021a40" src="/files/logicappblog5.png">

Come back [tomorrow and we'll wrap up the app!](http://www.michaelcrump.net/azure-tips-and-tricks39/). 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 