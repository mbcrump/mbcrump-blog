---
layout: post
title: "Azure Tips and Tricks Part 70 - Text Analysis with Cognitive Service and Azure"
excerpt: "Learn how to access text analysis with Cognitive Service and Azure"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Text Analysis with Cognitive Service and Azure

I recently took a look at Text Analysis that was introduced with Cognitive Services and is now inside the Azure portal. If you open the Azure portal and look for **AI and Cognitive Services** then you'll see the following:

<img style="border:3px solid #021a40" src="/files/aicog1.png">

Let's give **Text Analysis** a spin. Open the blade and fill out the following info. Be sure to select the **Free** tier (F0) as shown below:

<img style="border:3px solid #021a40" src="/files/aicog2.png">

Select **Keys** and copy the value of Key 1. 

<img style="border:3px solid #021a40" src="/files/aicog3.png">

We'll use [Postman](https://www.getpostman.com/) to test. Go ahead and download it if you haven't already and once complete you'll use one of the following endpoints depending on what you want to use. 

```text
https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/sentiment
https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases
https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages
```

We'll use **keyPhrases**, so copy the `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases` url into Postman and set the following three header properties:

* Ocp-Apim-Subscription-Key = should be your Key 1 (from our discussion earlier). 
* Content-Type = Set it to application/json.
* Accept = Set it to application/json.

Your screen should look like the following: 

<img style="border:3px solid #021a40" src="/files/aicog4.png">

Now switch over to **Body**, then **Raw** and post the following JSON (from some of my recent tweets):

```json
{
        "documents": [
            {
                "language": "en",
                "id": "1",
                "text": "Top 10 .NET Development Tweets that Broke the Web in 2017 - http://mcrump.me/2ot58Co  #dotnet"
            },
            {
                "language": "en",
                "id": "2",
                "text": "Setting up a managed container cluster with AKS and Kubernetes in the #Azure Cloud running .NET Core in minutes - http://mcrump.me/2op9mek  #dotnet"
            }
        ]
}
```

<img style="border:3px solid #021a40" src="/files/aicog5.png">

Now press **Send** and it will return key phrases from my tweets.

```json
{
    "documents": [
        {
            "keyPhrases": [
                "Web",
                ".NET Development Tweets",
                "dotnet"
            ],
            "id": "1"
        },
        {
            "keyPhrases": [
                "Kubernetes",
                "Azure Cloud",
                "minutes -",
                "AKS",
                ".NET Core"
            ],
            "id": "2"
        }
    ],
    "errors": []
}
```

As you can see it was very easy to get up and started. There obviously is a [couple of SDKs](https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/overview) that you can play with, but for now a quick test is all we need. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 