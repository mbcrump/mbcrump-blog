---
layout: post
title: "Azure Tips and Tricks Part 92 - Part 3 - Querying an Azure Search Index"
excerpt: "Learn how to query an Azure Search Index through the Azure Portal"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Implementing Azure Search with SQL Server and ASP.NET MVC

In this series I'll cover Azure Search, SQL Server and putting it all together in a ASP.NET MVC web app. The complete list can be found below:

* [Part 1 - Implementing Azure Search with SQL Server and ASP.NET MVC](http://www.michaelcrump.net/azure-tips-and-tricks90/)
* [Part 2 - Implementing Azure Search with SQL Server](http://www.michaelcrump.net/azure-tips-and-tricks91/)
* [Part 3 - Querying an Azure Search Index](http://www.michaelcrump.net/azure-tips-and-tricks92/)
* [Part 4 - Searching an index with Azure Search with C#](http://www.michaelcrump.net/azure-tips-and-tricks93/)


## Implementing Azure Search

This week we've learned that Azure Search is a search-as-a-service that connects to a variety of data sources such as SQL Server. We've created our SQL Server DB, and stood up Azure Search and now it is time to query the indexes. In this section, I'll give you some basic commands that should help get you started. 

Open the Azure Portal, and search for **Search Services** and click on the **Search Services** tab as shown below. 

<img style="border:3px solid #021a40" src="/files/azsearchfilter1.png">

Basic Search - I can type `search=john` and pressing **Search** to search the entire index for the word john. 

<img style="border:3px solid #021a40" src="/files/azsearchfilter2.gif">

Append strings - I can append onto the string with the **&** to pass additional search parameters, which can be specified in any order. For example, the  $count=true parameter returns a sum of all the documents that match the query. Make note that this is using OData.

<img style="border:3px solid #021a40" src="/files/azsearchfilter3.png">

Return top # - You can even pass **$top=2** to return the highest ranked 2 documents. 

<img style="border:3px solid #021a40" src="/files/azsearchfilter4.png">

Filtering - You can use the **$filter** parameter to return results matching the criteria you provided. For example, `$filter FirstName eq 'Robert'` would return any person in the index that has a FirstName that equals Robert. There are many other comparison expressions (such as eq, ne, gt, lt, ge, le). 

Order-by syntax - You can use the **$orderby** parameter to order the results by. You can use either asc or desc to explicitly specify the sort order. By default, it will use the sort order as ascending.

I'd encourage you to view the [OData Expression Syntax for Azure Search](https://docs.microsoft.com/en-us/rest/api/searchservice/odata-expression-syntax-for-azure-search) for a full list and other samples that you can use. 

Come back tomorrow and we'll start using a Console App to tie it all together. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 