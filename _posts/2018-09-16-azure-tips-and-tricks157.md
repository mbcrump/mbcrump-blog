---
layout: post
title: "Azure Tips and Tricks Part 157 - Part 1 Create Thumbnail Images with Azure Functions and Azure Storage"
excerpt: "Learn how to create a thumbnail images with Azure Functions and Azure Storage"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---
 
**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}
 
## Create Thumbnail Images with Azure Functions and Azure Storage 

In this mini-series, we're going to create an Azure Function that detects when a new image is added to Azure Storage and automatically creates a thumbnail image for us.

* [Azure Tips and Tricks Part 157 - Part 1 Create Thumbnail Images with Azure Functions and Azure Storage](http://www.michaelcrump.net/azure-tips-and-tricks157/)
* [Azure Tips and Tricks Part 158 - Part 2 Create Thumbnail Images with Azure Functions and Azure Storage](http://www.michaelcrump.net/azure-tips-and-tricks158/)

## Part 1 (Setup) Azure Portal
 
Go ahead and open the **Azure Portal** and click **Create a Resource** and select **Azure Storage**. We’ll keep it simple as shown below to get started.
 
<img style="border:3px solid #021a40" src="/files/imageresizer1.png">

Once complete, go into the resource and look under **Services**. 

<img style="border:3px solid #021a40" src="/files/storageacct2.png">

Go ahead and click on **Blobs** and create a **Container** and give it the name **originals** and then create another one called **thumbs**.

**Remember this!** Think of a container in this sense as a folder. https://myblob/**container**/image1.jpg
{: .notice--primary}

<img style="border:3px solid #021a40" src="/files/imageresizer2.png">

We're going to need our Access Key shortly, so look under **Settings**, then **Access Keys** and copy the **connection string** to your clipboard.

**What is an Access Key?** This string will allow us to connect to the Storage Account.
{: .notice--primary}

<img style="border:3px solid #021a40" src="/files/storagethroughcsharp1.png">

## Part 2 (Setup) Visual Studio

Create a C# Azure Function application by opening Visual Studio and selecting the template under the **Cloud** node as shown below:

<img style="border:3px solid #021a40" src="/files/imageresizer3.png">

Under Storage, change the default emulator to the **Azure Storage Account** that we created earlier:

<img style="border:3px solid #021a40" src="/files/imageresizer4.png">

We'll begin by using the **Timer Trigger** and **Azure Function v1** leaving everything as the defaults. 

<img style="border:3px solid #021a40" src="/files/imageresizer5.png">

Once the project spins up, we'll use NuGet to pull in references to :

* ImageResizer `A helper class for Image Resizing`

Looking good so far and a good stopping point for today. Come back soon for the next post in the series where we'll begin putting this all together. 

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
 
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.