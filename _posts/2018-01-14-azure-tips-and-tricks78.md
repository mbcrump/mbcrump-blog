---
layout: post
title: "Azure Tips and Tricks Part 78 - Copy Azure Storage Blobs and Files via C#"
excerpt: "Learn how to copy Azure Storage Blobs and Files via C#"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Developer Guide Book *2nd Edition available now!** This free eBook is available now at [aka.ms/azuredevebook](https://aka.ms/azuredevebook).
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Copy Azure Storage Blobs and Files via C#

Last week we've reviewed the following options with Azure Storage :

* [Working with Azure Storage Blobs and Files through the Portal](http://www.michaelcrump.net/azure-tips-and-tricks74/)
* [Create an Azure Storage Blob Container through C#](http://www.michaelcrump.net/azure-tips-and-tricks75/)
* [Uploading and Downloading a Stream into an Azure Storage Blob](http://www.michaelcrump.net/azure-tips-and-tricks76/)
* [Working with Azure Storage Explorer](http://www.michaelcrump.net/azure-tips-and-tricks77/)

Today, we are going to copy Azure Storage Blobs (and Files) via C#. Go ahead and open the Azure Portal and open the C# app that we worked with [earlier](http://www.michaelcrump.net/azure-tips-and-tricks75/).

The goal of this exercise is to copy a file inside our Azure Storage Container to a new file. So for example, our Azure Storage Container only contains one file now: 

<img style="border:3px solid #021a40" src="/files/storageacct4.png">

We are going to copy a new file inside of it with the name **mikepic-backup.png**. 

Now that we've created the Azure Storage Blob Container, we'll upload a file to it. We'll build off our [previous post](http://www.michaelcrump.net/azure-tips-and-tricks76/) and add the following lines of code to upload a file off our local hard disk:

```csharp
static void Main(string[] args)
{
    var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnection"));
    var myClient = storageAccount.CreateCloudBlobClient();
    var container = myClient.GetContainerReference("images-backup");
    container.CreateIfNotExists(BlobContainerPublicAccessType.Blob);

    var blockBlob = container.GetBlockBlobReference("mikepic.png");
//lines added
    var copyBlockBlob = container.GetBlockBlobReference("mikepic-backup.png");

    var cb = new AsyncCallback(x => Console.WriteLine("copy completed"));
    copyBlockBlob.BeginStartCopy(blockBlob, cb, null);
//end lines added

    Console.ReadLine();
}
```

If we run the application and switch over to our Storage Account and navigate inside the container, we'll see our file has copied successfully:

<img style="border:3px solid #021a40" src="/files/azasynccopy1.png">

Success!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 