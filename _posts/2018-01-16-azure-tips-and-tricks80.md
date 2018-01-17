---
layout: post
title: "Azure Tips and Tricks Part 80 - Adding Metadata to a file inside Azure Storage Blob Container"
excerpt: "Learn how to add metadata to a file inside Azure Storage Blob Container"
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

## Adding Metadata to a file inside Azure Storage Blob Container

We've reviewed the following options with Azure Storage so far:

* [Working with Azure Storage Blobs and Files through the Portal](http://www.michaelcrump.net/azure-tips-and-tricks74/)
* [Create an Azure Storage Blob Container through C#](http://www.michaelcrump.net/azure-tips-and-tricks75/)
* [Uploading and Downloading a Stream into an Azure Storage Blob](http://www.michaelcrump.net/azure-tips-and-tricks76/)
* [Working with Azure Storage Explorer](http://www.michaelcrump.net/azure-tips-and-tricks77/)
* [Copy Azure Storage Blobs and Files via C#](http://www.michaelcrump.net/azure-tips-and-tricks78/)
* [Creating an Azure Blob Hierarchy](http://www.michaelcrump.net/azure-tips-and-tricks79/)
* [Today - Adding Metadata to a file inside Azure Storage Blob Container](http://www.michaelcrump.net/azure-tips-and-tricks80/)

Today, we are going to look at setting user-defined metadata to a file inside an Azure Storage Blob Container via C#. Go ahead and open the Azure Portal and open the C# app that we worked with [earlier](http://www.michaelcrump.net/azure-tips-and-tricks75/). If you want to start from this post, then use the code located [here](https://github.com/mbcrump/azurestorage).

**What is User-defined metadata?** [User-defined metadata](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-properties-metadata) is metadata that you specify on a given resource in the form of a name-value pair. You can use metadata to store additional values with a storage resource. These additional metadata values are for your own purposes only, and do not affect how the resource behaves.*(courtesy of docs)*
{: .notice--info}

If you look below, you will notice that there is a way to do this inside the portal. 

<img style="border:3px solid #021a40" src="/files/azmetadata1.png">

You'll notice this is key-value pairs. 

<img style="border:3px solid #021a40" src="/files/azmetadata2.png">

We can also do this with code by adding as shown below.

```csharp
static void Main(string[] args)
{
var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnection"));
var myClient = storageAccount.CreateCloudBlobClient();
var container = myClient.GetContainerReference("images-backup");
//add method
SetMetadata(container);
//add method
Console.ReadLine();
}

static void SetMetadata(CloudBlobContainer container)
{
    // Add some metadata to the container.
    container.Metadata.Clear();
    container.Metadata.Add("Owner", "Michael Crump");
    container.Metadata["LastUpdated"] = DateTime.Now.ToString();
    container.SetMetadata();
}
```

This method clears the metadata and add the key-value pair that we talked about earlier. 

We can also write a **GetMetadata** method to retrieve metadata from our container.

```csharp
static void GetMetadata(CloudBlobContainer container)
{
    container.FetchAttributes();
    foreach (var item in container.Metadata)
    {
        Console.WriteLine(
        string.Format("{0}: {1}", item.Key, item.Value));
    }
}
```

If we run the application and look at our console output, then we'll see the following:

<img style="border:3px solid #021a40" src="/files/azmetadata3.png">

Success! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 