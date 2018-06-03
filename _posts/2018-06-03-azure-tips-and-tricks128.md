---
layout: post
title: "Azure Tips and Tricks Part 128 - Download all Azure Documentation for offline viewing"
excerpt: "Learn how to quickly download all of the Azure documentation for offline viewing"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Check out Azure.Source by [Rob Caron](https://twitter.com/RobCaronMSFT)** : A very nice mix of Azure news, announcements, videos, podcast and more. [Read weekly](https://azure.microsoft.com/en-us/blog/azure-source-volume-33/)
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Download all Azure Documentation for offline viewing

There have been several times when I've wished to have all the Azure documentation on my local computer whether it be a flight, etc.. I've never found a way except finding the [pieces of the documentation](https://docs.microsoft.com/en-us/azure/security-center/) that I wanted and pressing the **Download PDF** button. 

<img style="border:3px solid #021a40" src="/files/documentation1.png">

Until Now... 

If you want to download **ALL** of the Azure documentation, then follow the instructions below: 

1.) You'll need to first download [jq](https://stedolan.github.io/jq/download/) with is a JSON processor. If you have a Mac, then you can use `brew install jq`  or on Windows use Chocolatey NuGet `chocolatey install jq`. Sample output from my machine is below:

```text
Michaels-MBP:Documents mbcrump$ brew install jq
==> Installing jq
==> Downloading https://homebrew.bintray.com/bottles/jq-1.5_3.high_sierra.bottle
######################################################################## 100.0%
==> Pouring jq-1.5_3.high_sierra.bottle.tar.gz /usr/local/Cellar/jq/1.5_3: 19 files, 946.6KB
```

2.) Next you'll need to run the following command which uses curl and jq to download every PDF contained in the [GitHub repo](https://api.github.com/repositories/72685026/contents/articles): 

```text
curl https://api.github.com/repositories/72685026/contents/articles | jq -r '.[] | select(.type | contains("dir")) | "https://docs.microsoft.com/pdfstore/en-us/Azure.azure-documents/live/\(.name).pdf"' | wget -i -
```

3.) Give it some time as it is about 2GB and check the folder where you ran that command. 

<img style="border:3px solid #021a40" src="/files/documentation2.png">

4.) Success! You'll see all the PDF file and you now have a current snapshot of Azure's documentation.

<img style="border:3px solid #021a40" src="/files/documentation3.png">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 