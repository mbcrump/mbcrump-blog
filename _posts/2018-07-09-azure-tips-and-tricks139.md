---
layout: post
title: "Azure Tips and Tricks Part 139 - Prevent AzCopy Uploads from maxing out Internet Connection Speed"
excerpt: "Learn how to prevent AzCopy uploads from maxing out internet connection speed"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Prevent AzCopy Uploads from maxing out Internet Connection Speed

**What is AzCopy?** AzCopy is a command-line utility designed for copying data to/from Microsoft Azure Blob, File, and Table storage, using simple commands designed for optimal performance. You can copy data between a file system and a storage account, or between storage accounts. *(courtesy of docs)*
{: .notice--info}

You can download either the latest version of AzCopy on [Windows](http://aka.ms/downloadazcopy) or [Linux](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-linux).

For this example, I'm going to use Windows. If you type AzCopy then you'll see there is a list of parameters available. 

<img style="border:3px solid #021a40" src="/files/azcopy1blog.png">

At first glance, you may think this is all but you can easily type `azcopy /?` to get a complete list which will show you additional parameters - which includes the one that we'll talk about shortly. 

If you are using **AzCopy** to send large amounts of data to Azure on either a residential or small business internet pipe, or if for whatever reason you want to limit the concurrent-operations that the app uses then this tip is for you. 

Simply use the `/NC:"number-of-concurrent-operations"` where `number-of-concurrent-operations` specifies the number of concurrent operations. (for example: azcopy /NC:1)

```text
AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput. Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing. Throttle concurrent operations based on actual available network bandwidth.

The upper limit for concurrent operations is 512.

Applicable to: Blobs, Files, Tables
```

For a complete list of parameters and additional information then visit [docs](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#azcopy-parameters)

I hope this helps!


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 