---
layout: post
title: "Azure Tips and Tricks Part 152 - Get the Record Count in Cosmos DB"
excerpt: "Learn how to get the record count in Azure Cosmos DB"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Get the Record Count in Cosmos DB

When working with Azure Cosmos DB, it is guaranteed that at some point that you'll need to get the record count of a document. There are a couple of quick ways of how to do this through the Azure Portal by navigating to the Cosmos DB resource you wish to query and selecting the **Data Explorer** tab and using the following query: `SELECT VALUE COUNT(1) FROM c`

<img style="border:3px solid #021a40" src="/files/dataexpcosmos1.png">

> If you’re wondering about the VALUE keyword – all queries return JSON fragments back. By using VALUE, you can get the scalar value of count e.g., 100, instead of the JSON document {"$1": 100}

You may want to know the **Request Charge** for that query and you can see that by clicking on **Query Information**. 

<img style="border:3px solid #021a40" src="/files/dataexpcosmos2.png">

If you compare that to some of the older methods folks used before `COUNT` was available such as `SELECT c.id FROM c` then you'd see that it might be time to update the queries. 

<img style="border:3px solid #021a40" src="/files/dataexpcosmos3.png">

If I need to put this logic inside of an application instead of access it through the Azure Portal, here is how I do that in C#. 

First, I create a `app.config` file and add the following appSettings tags.

>You can get the **endpoint** and **authkey** from the **Keys** section in your Cosmos DB blade in the portal. 

```text
<appSettings>
    <add key="endpoint" value="enter" />
    <add key="authkey" value="enter" />
    <add key="database" value="enter" />
    <add key="collection" value="enter" />
  </appSettings>
  ```


```csharp

private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
private static readonly string EndPointId = ConfigurationManager.AppSettings["endpoint"];
private static readonly string AuthKeyId = ConfigurationManager.AppSettings["authkey"];

private static DocumentClient client;

client = new DocumentClient(new Uri(EndPointId), AuthKeyId);
CreateDatabaseIfNotExistsAsync().Wait();
CreateCollectionIfNotExistsAsync().Wait();

FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

IQueryable<dynamic> familyQueryInSql = client.CreateDocumentQuery<dynamic>(
UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId),
    "SELECT VALUE COUNT(1) FROM c",
    queryOptions);

Console.WriteLine("Running direct SQL query...");
foreach (dynamic family in familyQueryInSql)
{
    Console.WriteLine("\tRead {0}", family);
}

Console.Read();
```

<img style="border:3px solid #021a40" src="/files/dataexpcosmos4.png">

Success!!

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 