---
layout: post
title: "Azure Tips and Tricks Part 85 - Updating an item from a Azure Storage Table"
excerpt: "Learn how to update an item from an Azure Storage Table"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Developer Guide Book 2nd Edition available now!** This free eBook is available now at [aka.ms/azuredevebook](https://aka.ms/azuredevebook).
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Updating an item from a Azure Storage Table

In case you are new to the Azure Storage Tables, we've reviewed the following items this week:

* [Creating your first Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks82/)
* [Adding an item to a Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks83/)
* [Reading an item from a Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks84/)
* [Today - Updating an item from a Azure Storage Table](http://www.michaelcrump.net/azure-tips-and-tricks85/)

Today, we'll be taking a look at updating an item through C# code into an Azure Storage Table. 

## Getting Started

Open the C# Console application that we were working with [yesterday](http://www.michaelcrump.net/azure-tips-and-tricks84/) and let's add a method to:

* Update an item based off of the table, RowKey and PartitionKey that we pass in.

## Update an item

In our `Program.cs` file, we'll now add in a helper method that passes in a table, RowKey and PartitionKey.

```csharp
    static Thanks UpdateMessage(CloudTable table, string partitionKey, string rowKey)
    {
        TableOperation retrieve = TableOperation.Retrieve<Thanks>(partitionKey, rowKey);

        TableResult result = table.Execute(retrieve);

        return (Thanks)result.Result;
    }
```

In this example, we're passing in the table name, a partition key and a row key to return a message that we'll update shortly. Make a note that this uses the **Retrieve** method that we haven't worked with before. Now we'll have an instance of the record that we want to update. 


## Putting it all together

The **Main** method inside of the `Program.cs` file needs to specify which table, RowKey and PartitionKey that we want to update and then if it is not null, then we want to update the message with the one that we specify. We finally call the **TableOperation** method to update the message. 

```csharp
static void Main(string[] args)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
                    CloudConfigurationManager.GetSetting("StorageConnection"));

    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

    CloudTable table = tableClient.GetTableReference("thankfulfor");

    table.CreateIfNotExists();

    //added these lines

    var message = UpdateMessage(table, "ThanksApp", "I'm thankful for the time with my family");

    if (message != null)
    {
        message.Name = "I'm thankful for the time with my family AND friends!";
    }

    TableOperation update = TableOperation.Replace(message);

    //added these lines

    table.Execute(update);
    Console.ReadKey();

}
```

<img style="border:3px solid #021a40" src="/files/azupdatetable1.gif">

If we run the program now, then it will update the messages with the new text that we specified. As described yesterday, you can use the [Azure Storage Explorer](http://www.michaelcrump.net/azure-tips-and-tricks77/) if you don't need access to the table through code.  If you come back tomorrow, then I'll show you how to delete this item through code. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 