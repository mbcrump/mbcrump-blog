---
layout: post
title: "Azure Tips and Tricks Part 34 - Working with the Azure CLI using a Mac"
excerpt: "Learn how to work with the Azure CLI 2.0 using a Mac"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Working with the Azure CLI using a Mac

The **Azure CLI 2.0** provides a command-line experience for managing Azure resources. You can use it with Azure Cloud Shell which sits inside your web browser, or you can install it on macOS, Linux, and Windows. In this post, we'll install it on a Mac. 
{: .notice--info}

My preferred way to work with the Azure CLI 2.0 on a Mac is to have [Homebrew](https://brew.sh/) installed. Basically, homebrew is a package manager for Mac that makes it easy to install application. 

Once it is installed, you'll want to run these two commands:

```bash
brew update
brew install azure-cli
``` 

The first command just updates the homebrew database and the next command installs the Azure CLI 2.0 as shown below. 

<img style="border:3px solid #021a40" src="/files/climac1.gif">

Wow, that was pretty easy! You can type `az -h` to get help documentation or go to [aka.ms/cli](https://aka.ms/cli) to read the docs.

### Log in to Azure

You'll want to use the `az login` command to log in to your Azure account. You'll see the following message:

```text
To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the code XXX to authenticate.
```

Open a web browser and navigate to https://aka.ms/devicelogin and enter your code. You'll be prompted to enter the code to authenticate. 

<img style="border:3px solid #021a40" src="/files/azuredevlogin.png">


Switch back to the terminal app and you'll see something similar to the following if you logged in successfully:

```text
[
  {
    "cloudName": "AzureCloud",
    "id": "xxx",
    "isDefault": true,
    "name": "Visual Studio Enterprise",
    "state": "Enabled",
    "tenantId": "xxx",
    "user": {
      "name": "micrum@email.com",
      "type": "user"
    }
  }
]
```

Keep in mind that you can always get back to this screen with `az account` list. You can now try to create a Ubuntu VM using only the CLI. [Here](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli) is a great doc to get started. 

Make sure to read the complete [CLI docs](https://docs.microsoft.com/en-us/cli/azure/overview) to learn more. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--inverse} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 