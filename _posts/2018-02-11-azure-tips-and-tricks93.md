---
layout: post
title: "Azure Tips and Tricks Part 92 - Part 4 - Searching an index with Azure Search with C#"
excerpt: "Learn how to query an Azure Search Index using C#"
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

Last week we've learned that Azure Search is a search-as-a-service that connects to a variety of data sources such as SQL Server. We've created our SQL Server DB, and stood up Azure Search and even query the index through the Azure Portal. In this final section, we'll work with C# and query the index.

Open the Azure Portal, and search for **Search Services** and click on the **Search Services** that we created earlier and look for **Keys**. Copy and paste the key b/c we'll be using it shortly. 

<img style="border:3px solid #021a40" src="/files/part4azsearch.png">

You'll also want to remember the name of your search service. In my case it is - mcadventureworks 

Once that is complete, head into Visual Studio and create a Console Application. Use NuGet to pull in references to **Microsoft.Azure.Search** as shown below. 

<img style="border:3px solid #021a40" src="/files/part4azsearch1.png">

Add the following code to **Program.cs** to search the index:

```csharp
static void Main(string[] args)
{

    var searchServiceName = "yoursearchservice";
    var apiKey = "yourapikey";

    var searchClient = new SearchServiceClient(searchServiceName, new SearchCredentials(apiKey));
    var indexClient = searchClient.Indexes.GetClient("azuresql-index"); //check this to match your index

    DocumentSearchResult<MySQLDB> results;

    Console.WriteLine("Search the entire index for the term 'Michael' \n");

    results = indexClient.Documents.Search<MySQLDB>("Michael");

    WriteDocuments(results);

    Console.Read();
}

private static void WriteDocuments(DocumentSearchResult<MySQLDB> searchResults)
{
    foreach (SearchResult<MySQLDB> result in searchResults.Results)
    {
        Console.WriteLine(result.Document.FirstName + " " + result.Document.LastName);
    }

    Console.WriteLine();
}
```

Create a class named **MySQLDB** and add the following:

```csharp

[SerializePropertyNamesAsCamelCase]
class MySQLDB
{
    [IsFilterable, IsSortable, IsFacetable]
    public string CustomerID { get; set; }
    [IsFilterable, IsSortable, IsFacetable]
    public string FirstName { get; set; }
    [IsFilterable, IsSortable, IsFacetable]
    public string LastName { get; set; }
    [IsFilterable, IsSortable, IsFacetable]
    public string EmailAddress { get; set; }
    [IsFilterable, IsSortable, IsFacetable]
    public string ModifiedDate { get; set; }
    
}
```

When you run the app, it will search the entire index for the term 'Michael' and display the results in your Console window. If you've followed the tutorial so far, then you should get around 17 results. 

```text
Search the entire index for the term 'Michael'

Michael Blythe
Michael Blythe
Michael Bohling
Michael Vanderhyde
Michael Vanderhyde
Michael Galos
Michael Galos
Michael Brundage
Michael Brundage
Michael Graff
Michael Graff
Michael Sullivan
Michael Sullivan
Michael Lee
Michael Lee
Michael John Troyer
Michael John Troyer
```

Until next time, happy coding!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 