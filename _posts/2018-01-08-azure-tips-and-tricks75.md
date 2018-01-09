---
layout: post
title: "Azure Tips and Tricks Part 75 - Create an Azure Storage Blob Container through C#"
excerpt: "Learn how to create an Azure Storage Blobs Container with C#"
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

## Create an Azure Storage Blob Container through C#

Azure Storage is described as a service that provides storages that is available, secure, durable, scalable, and redundant. Azure Storage consists of 1) Blob storage, 2) File Storage, and 3) Queue storage. In this post, we'll take a look at creating an Azure Storage Blob container with C#. [Yesterday](http://www.michaelcrump.net/azure-tips-and-tricks74/), I described how to do it through the Azure Portal. 

Go ahead and open the Azure Portal and navigate to the Azure Storage account that we worked with [yesterday](http://www.michaelcrump.net/azure-tips-and-tricks74/).

Look under **Settings**, then **Access Keys** and copy the connection string. 

<img style="border:3px solid #021a40" src="/files/storagethroughcsharp1.png">

Create a C# Console Application, and use NuGet to pull in references to :

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
    var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnection"));
    var myClient = storageAccount.CreateCloudBlobClient();
    var container = myClient.GetContainerReference("images-backup");
    container.CreateIfNotExists(BlobContainerPublicAccessType.Blob);
    Console.ReadLine();
}
```

This code will get our connection string from the **App.config**, create our client and a container named **images-backup** if it doesn't exist. We can go back inside of the portal to see if executed correctly. 

<img style="border:3px solid #021a40" src="/files/storagethroughcsharp4.png">

Success! We've now accomplished the same task via the Azure Portal and C#.

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 