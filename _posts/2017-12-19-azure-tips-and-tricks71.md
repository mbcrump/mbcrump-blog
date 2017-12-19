---
layout: post
title: "Azure Tips and Tricks Part 71 - Language Detection with Cognitive Service and Azure"
excerpt: "Learn how to access text analysis such as language detection with Cognitive Service and Azure"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Language Detection with Cognitive Service and Azure

After reviewing the [Text Analysis API](https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/overview), I noticed three capabilities that I wanted to take a further look at: 

* Sentiment Analysis - Find out what customers think of your brand or topic by analyzing raw text for clues about positive or negative sentiment. 
* [Key Phrase Detection](https://www.michaelcrump.net/azure-tips-and-tricks70/) - Automatically extract key phrases to quickly identify the main points. 
* [This post - Language Detection](https://www.michaelcrump.net/azure-tips-and-tricks71/) - For up to 120 languages, detect which language the input text is written in and report a single language code for every document submitted on the request. 

In this post, we'll look at Language Detection which is part of Cognitive Services and is now inside the Azure portal. 

If you open the Azure portal and look for **AI and Cognitive Services** then you'll see the **Text Analysis API** that we worked with yesterday and we'll continue using it today. Open the blade and fill out the following info if you didn't do this yesterday. Be sure to select the **Free** tier (F0) as shown below:

<img style="border:3px solid #021a40" src="/files/aicog2.png">

Select **Keys** and copy the value of KEY 1 if you don't already have this. 

<img style="border:3px solid #021a40" src="/files/aicog3.png">

## Working with Language Detection and Postman

We need an endpoint to begin calling the API, if you look at the **Overview** option inside your cognitive service, then you'll see the following: 

<img style="border:3px solid #021a40" src="/files/aicog6.png">

While that is the endpoint, it is missing the feature of the Text Analysis that you might want to call. A complete list is below:  

```text
sentiment
keyPhrases
languages
```

We want to use the **languages** endpoint for this tutorial. 

**What are languages?** This feature detects which language the input text is written in and report a single language code for every document submitted on the request. The language code is paired with a score indicating the strength of the score.
{: .notice--primary}

Copy the `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages` url into Postman and set the following three header properties:

* Ocp-Apim-Subscription-Key = should be your Key 1 (from our discussion earlier). 
* Content-Type = Set it to `application/json`.
* Accept = Set it to `application/json`.

Your screen should look like the following: 

<img style="border:3px solid #021a40" src="/files/aicog7.png">

Now switch over to **Body**, then **Raw** and post the following JSON:

```json
 {
     "documents": [
         {
             "id": "1",
             "text": "Azure Tips and Tricks - English"
         },
         {
             "id": "2",
             "text": "Consejos y trucos de Azure - Inglés"
         },
         {
             "id": "3",
             "text": "하늘빛 팁과 트릭 - 영어"
         }               
     ]
 }
```

id 1 is obviously English, 2 is Spanish and 3 is Korean language. 

<img style="border:3px solid #021a40" src="/files/aicog8.png">

Now press **Send** and it will return the languages detected.

```json
{
  "documents": [{
    "id": "1",
    "detectedLanguages": [{
      "name": "English",
      "iso6391Name": "en",
      "score": 1.0
    }]
  }, {
    "id": "2",
    "detectedLanguages": [{
      "name": "Spanish",
      "iso6391Name": "es",
      "score": 1.0
    }]
  }, {
    "id": "3",
    "detectedLanguages": [{
      "name": "Korean",
      "iso6391Name": "ko",
      "score": 1.0
    }]
  }],
  "errors": []
}
```

I hope you find this helpful! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 