---
layout: post
title: "Azure Tips and Tricks Part 95 - Access all files from an Azure Storage Blob Container"
excerpt: "Learn how to get all Files from an Azure Storage Blob Container"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Get all Files from an Azure Storage Blob Container

Azure Storage is described as a service that provides storages that is available, secure, durable, scalable, and redundant. Azure Storage consists of 1) Blob storage, 2) File Storage, and 3) Queue storage. In the past [posts](http://www.michaelcrump.net/azure-tips-and-tricks74/), I've described how to create an Azure Storage account through the Portal and [how to](http://www.michaelcrump.net/azure-tips-and-tricks75/)  create an Azure Storage Blob Container through C#. I've even detailed how to upload and download a stream into an Azure Storage Blob](http://www.michaelcrump.net/azure-tips-and-tricks76/) but I've always grabbed one file at a time. In this post, I'll show you how you can quickly access **all the files of a given extension** in a container instead of a single one. 

## Download a Single File in an Azure Storage Blob Container

If you have an existing container and know the filename, then you can use this code (which was covered before) to grab a single file.

```csharp
static void Main(string[] args)
{
    var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnection"));
    var myClient = storageAccount.CreateCloudBlobClient();
    var container = myClient.GetContainerReference("images-backup");
    container.CreateIfNotExists(BlobContainerPublicAccessType.Blob);

    var blockBlob = container.GetBlockBlobReference("mikepic.png");
    using (var fileStream = System.IO.File.OpenWrite(@"C:\Users\mbcrump\Downloads\mikepic-backup.png"))
    {
      blockBlob.DownloadToStream(fileStream);
    }

    Console.ReadLine();
}
```

## Download all File Extensions in an Azure Storage Blob Container

If you have an existing container and want to pull down all the files for a specific type, then you can use this code.

```csharp
    var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnection"));
    var myClient = storageAccount.CreateCloudBlobClient();
    var container = myClient.GetContainerReference("images-backup");
    container.CreateIfNotExists(BlobContainerPublicAccessType.Blob);

    var list = container.ListBlobs();
    var blobs = list.OfType<CloudBlockBlob>().Where(b => Path.GetExtension(b.Name).Equals(".png")); 
    
    foreach (var item in blobs)
    {
        string name = ((CloudBlockBlob)item).Name;
        CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
        string path = (@"C:\Users\mbcrump\Downloads\test\" + name);
        blockBlob.DownloadToFile(path, FileMode.OpenOrCreate);
    }

    Console.ReadLine();
```

Simple enough!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 