---
layout: post
title: "Azure Tips and Tricks Part 82 - Creating your first Azure Storage Table"
excerpt: "Learn how to creating your first Azure Storage Table"
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

## Creating your first Azure Storage Table

In case you are new to the Azure Storage, we've reviewed the following options so far:

* [Working with Azure Storage Blobs and Files through the Portal](http://www.michaelcrump.net/azure-tips-and-tricks74/)
* [Create an Azure Storage Blob Container through C#](http://www.michaelcrump.net/azure-tips-and-tricks75/)
* [Uploading and Downloading a Stream into an Azure Storage Blob](http://www.michaelcrump.net/azure-tips-and-tricks76/)
* [Working with Azure Storage Explorer](http://www.michaelcrump.net/azure-tips-and-tricks77/)
* [Copy Azure Storage Blobs and Files via C#](http://www.michaelcrump.net/azure-tips-and-tricks78/)
* [Creating an Azure Blob Hierarchy](http://www.michaelcrump.net/azure-tips-and-tricks79/)
* [Adding Metadata to a file inside Azure Storage Blob Container](http://www.michaelcrump.net/azure-tips-and-tricks80/)
* [Working with AzCopy and Azure Storage](http://www.michaelcrump.net/azure-tips-and-tricks81/)

While we've been working with Azure Storage Blobs and Files, we'll switch this week to taking a look at Azure Storage Tables. 

**What is Azure Storage Tables?** They are a NoSQL key-value store for rapid development using massive semi-structured datasets*
{: .notice--info}

As a refresher, Azure Storage Blobs can store any type of text or binary data, such as a document, media file, or application installer. Blob storage is also referred to as object storage.

So to recap, think of Azure Storage Tables as key-value data set that you can query vs. Azure Storage Blobs which are typically files. 

## Getting Started

Go ahead and open the Azure Portal and click **Create a Resource** and select **Azure Storage**. We'll keep it simple as shown below to get started. 

<img style="border:3px solid #021a40" src="/files/storageacct1.png">

Once complete, go into the resource and look under **Services**. 

<img style="border:3px solid #021a40" src="/files/storageacct2.png">

Go ahead and click on **Tables** and you could create a new table through the portal as shown below.

<img style="border:3px solid #021a40" src="/files/aztablesblog1.png">

If we did that, then we'd see a table alongwith the URL that it is accessible from. 

<img style="border:3px solid #021a40" src="/files/aztablesblog2.png">

While this is good and fine, we'd like to create the table dynamically to represent a real-world scenario. 

For this example, we'll use C#. 

While inside the blade for Azure Storage, look under **Settings**, then **Access Keys** and copy the connection string. 

<img style="border:3px solid #021a40" src="/files/storagethroughcsharp1.png">

Create a C# Console Application using Visual Studio, and use NuGet to pull in references to :

* WindowsAzure.Storage
* Microsoft.WindowsAzure.ConfigurationManager

<img style="border:3px solid #021a40" src="/files/storagethroughcsharp2.png">
<img style="border:3px solid #021a40" src="/files/storagethroughcsharp3.png">

Inside of your Console app, you will see **App.config**, now add the following section:

```text
  <appSettings>
    <add key="StorageConnection" value="YOUR-CONNECTION-STRING-COPIED-FROM-EARLIER"/>
  </appSettings>
```

Copy the following code into your Main method:

```csharp
static void Main(string[] args)
{
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
                CloudConfigurationManager.GetSetting("StorageConnection"));
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("thankfulfor");
table.CreateIfNotExists();
Console.ReadKey();
}
```

This code will get our connection string from the **App.config**, create our client and a table named **thankfulfor** if it doesn't exist. We can go back inside of the portal to see if executed correctly. 

<img style="border:3px solid #021a40" src="/files/aztablesblog3.png">

Looking good so far! Now that we've created a table, let's begin adding some data to it. Come back tomorrow or look at the [master list](https://michaelcrump.net/azure-tips-and-tricks-complete-list/) if you aren't following day by day. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 