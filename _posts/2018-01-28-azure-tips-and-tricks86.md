---
layout: post
title: "Azure Tips and Tricks Part 86 - Deleting an item from a Azure Storage Table"
excerpt: "Learn how to delete an item from an Azure Storage Table"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Community Spotlight** I'd like to call out folks in this section that contribute to the Azure platform. Whether it be IT Pro or Developer, you should give this person a follow to stay up to date with their corner of Azure. 
  
[Scott Cate](https://twitter.com/ScottCate) works at Microsoft and is part of the Azure Cloud Developer Advocates team that focuses on .NET and Xamarin. Learn more about Scott [here](https://developer.microsoft.com/en-us/advocates/scott-cate) or follow him on [Twitter](https://twitter.com/ScottCate) .
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Deleting an item from a Azure Storage Table

In case you are new to the Azure Storage Tables, we've reviewed the following items this week:

* [Creating your first Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks82/)
* [Adding an item to a Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks83/)
* [Reading an item from a Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks84/)
* [Updating an item from a Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks85/)
* [Deleting an item from a Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks86/)]

Today, we'll be taking a look at deleting an item through C# code into an Azure Storage Table. 

## Getting Started

Open the C# Console application that we were working with [last week](http://www.michaelcrump.net/azure-tips-and-tricks85/) and let's add a method to:

* Delete an item based off of the table, RowKey and PartitionKey that we pass in.

## Delete an item

In our `Program.cs` file, we'll now add in a helper method that passes in a table, RowKey and PartitionKey to identify the message we want to delete.


```csharp
static void DeleteMessage(CloudTable table, string partitionKey, string rowKey)
{
    TableOperation retrieve = TableOperation.Retrieve<Thanks>(partitionKey, rowKey);

    TableResult result = table.Execute(retrieve);

    var deleteEntity = (Thanks)result.Result;

    TableOperation delete = TableOperation.Delete(deleteEntity);

    table.Execute(delete);
}
```

In this example, we retrieve the message and then delete the entity.

## Putting it all together.

The **Main** method inside of the `Program.cs` file, we'll call our helper method. 

```csharp
static void Main(string[] args)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
                    CloudConfigurationManager.GetSetting("StorageConnection"));

    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

    CloudTable table = tableClient.GetTableReference("thankfulfor");

    table.CreateIfNotExists();

    //added these lines
    DeleteMessage(table, "ThanksApp", "I'm thankful for the time with my family");
    //added these lines

    table.Execute(update);
    Console.ReadKey();

}
```

If we run the program now, then it will delete the message that we specified. As described earlier, you can use the [Azure Storage Explorer](http://www.michaelcrump.net/azure-tips-and-tricks77/) if you don't need access to the table through code.  If you come back tomorrow, then I'll show you how to delete this item through code. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 