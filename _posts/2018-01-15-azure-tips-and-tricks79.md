---
layout: post
title: "Azure Tips and Tricks Part 79 - Creating an Azure Blob Hierarchy"
excerpt: "Learn how to creating an Azure blob hierarchy"
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

## Creating an Azure Blob Hierarchy

We've reviewed the following options with Azure Storage so far:

* [Working with Azure Storage Blobs and Files through the Portal](http://www.michaelcrump.net/azure-tips-and-tricks74/)
* [Create an Azure Storage Blob Container through C#](http://www.michaelcrump.net/azure-tips-and-tricks75/)
* [Uploading and Downloading a Stream into an Azure Storage Blob](http://www.michaelcrump.net/azure-tips-and-tricks76/)
* [Working with Azure Storage Explorer](http://www.michaelcrump.net/azure-tips-and-tricks77/)
* [Copy Azure Storage Blobs and Files via C#](http://www.michaelcrump.net/azure-tips-and-tricks78/)

Today, we are going to look at creating an Azure blob hierarchy via C#. Go ahead and open the Azure Portal and open the C# app that we worked with [earlier](http://www.michaelcrump.net/azure-tips-and-tricks75/). If you want to start from this post, then use the code located [here](https://github.com/mbcrump/azurestorage).

The goal of this exercise is to create a blob hierarchy or folder structure inside of our container. So for example, we'd like to place a file in a structure such as such as **backup/images-backup.png**. 
{: .notice--info}

If you look below, you will notice that there is no way to create a folder structure from inside the portal. 

<img style="border:3px solid #021a40" src="/files/blobfolder1.png">

But we can easily do this with code by adding the folder structure we want into the code as shown below.

```csharp
static void Main(string[] args)
{
 var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnection"));
 var myClient = storageAccount.CreateCloudBlobClient();
 var container = myClient.GetContainerReference("images-backup");
 container.CreateIfNotExists(BlobContainerPublicAccessType.Blob);

// line modified
 var blockBlob = container.GetBlockBlobReference("backup/mikepic.png");
 using (var fileStream = System.IO.File.OpenRead(@"c:\mikepic.png"))
 {
    blockBlob.UploadFromStream(fileStream);
 }
 // line modified

 Console.ReadLine();
}
```

If we run the application and switch over to our Storage Account and navigate inside the container, we'll see our container now has a folder:

<img style="border:3px solid #021a40" src="/files/blobfolder2.png">

Success! Again, the source code is located [here](https://github.com/mbcrump/azurestorage).

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 