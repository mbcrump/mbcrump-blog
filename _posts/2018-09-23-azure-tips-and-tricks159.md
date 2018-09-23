---
layout: post
title: "Azure Tips and Tricks Part 159 - Use Azure Logic Apps and CosmosDB to monitor and archive Twitter hashtags"
excerpt: "Learn how to use Azure Logic Apps and CosmosDB to monitor and archive Twitter hashtags"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---
 
**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}
 
## Use Azure Logic Apps and CosmosDB to monitor and archive Twitter hashtags

I love data and use it constantly to improve everything in my personal life as well as my professional life. As we are about to begin the Microsoft Ignite conference, I wanted to collect tweets that use the #MSIgnite hashtag and save them to a database. I also don't want to code as I'm working on 3 sessions right now. Here's how I did it. 

## Create an Cosmos DB instance

Inside of the Azure Portal, create a Cosmos DB instance. 

For Cosmos DB :

* Use **SQL** for the API
* For Database ID use **cosmosdb-ignite**
* For Collection ID use **items**
* Throughput use **400**

<img style="border:3px solid #021a40" src="/files/azlogiccosmos1.png">
<img style="border:3px solid #021a40" src="/files/azlogiccosmos3.png">

## Create an Logic App instance

Inside of the Azure Portal, create a Logic App instance per the screenshot below

<img style="border:3px solid #021a40" src="/files/azlogiccosmos2.png">

## Logic App Designer

Open the Logic App that you just created and select **When a new tweet is posted** and log in with your Twitter credentials and select the interval and text you wish to search for. In my case I'm using #MSIgnite.  

<img style="border:3px solid #021a40" src="/files/azlogiccosmos4.png">

Choose an action that is **Create or update document**

<img style="border:3px solid #021a40" src="/files/azlogiccosmos5.png">

Provide the Connection Name (anything you want) and the account you wish to use. 

<img style="border:3px solid #021a40" src="/files/azlogiccosmos6.png">

Fill out the following fields:

* For Database ID use **cosmosdb-ignite**
* For Collection ID use **items**
* For Document use:

```text
{
  "created": @{triggerBody()?['CreatedAtIso']},
  "id": @{triggerBody()?['TweetId']},
  "text": @{triggerBody()?['TweetText']},
  "user": "@{triggerBody()?['TweetedBy']}"
}
```

Please note that these are dynamic fields, so you might not be able to copy and paste that text. 
{: .notice--primary}

<img style="border:3px solid #021a40" src="/files/azlogiccosmos7.png">

Click Save and then go into your Cosmos DB Instance and you can query the database to see the data coming in. 

<img style="border:3px solid #021a40" src="/files/azlogiccosmos8.png">

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
 
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.