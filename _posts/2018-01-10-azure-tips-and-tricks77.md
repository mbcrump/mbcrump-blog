---
layout: post
title: "Azure Tips and Tricks Part 77 - Working with Azure Storage Explorer"
excerpt: "Learn how to work with Azure Storage Explorer"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Want to Contribute?** I'm currently looking for folks who want to contribute to Azure Tips and Tricks. If you are interested, then [fill out the form here](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUQU9JMzJKVEVFVzdHRDNBWU9QVjROTUlKVS4u).
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Working with Azure Storage Explorer

This week we've reviewed the following options with Azure Storage :

* [Working with Azure Storage Blobs and Files through the Portal](http://www.michaelcrump.net/azure-tips-and-tricks74/)
* [Create an Azure Storage Blob Container through C#](http://www.michaelcrump.net/azure-tips-and-tricks75/)
* [Uploading and Downloading a Stream into an Azure Storage Blob](http://www.michaelcrump.net/azure-tips-and-tricks76/)

While it has been easy working with Azure Storage through the Portal and C#, one gem that I haven't covered was Azure Storage Explorer. In this post, we'll take a look at it. 

**What is it?** [Azure Storage Manager](https://azure.microsoft.com/en-us/features/storage-explorer/) allows you to easily manage the contents of your storage account. It comes complete with features such as: upload, download, and manage blobs, files, queues, tables, and Cosmos DB entities.
{: .notice--primary}

## How I typically work with Azure Storage Explorer

After downloading the tool, I typically begin with the option **Use a connection string or a shared access signature URI** as shown below. 

<img style="border:3px solid #021a40" src="/files/azstorageexp1.png">

I then switch over to my Azure Storage account that I want to work with and look under **Settings**, then **Access Keys** and copy the connection string to my clipboard. 

<img style="border:3px solid #021a40" src="/files/storagethroughcsharp1.png">

I paste that into Azure Storage Explorer and now have access to my data. 

<img style="border:3px solid #021a40" src="/files/azstorageexp2.png">

Now, I can do things such for my table storage such as CRUD operations as well as querying. 

<img style="border:3px solid #021a40" src="/files/azstorageexp3.gif">

It is absolutely terrific tool that works on various platforms (Windows, Mac, Linux) and keep in mind that it works with blobs, files, queues, tables, and Cosmos DB entities. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 