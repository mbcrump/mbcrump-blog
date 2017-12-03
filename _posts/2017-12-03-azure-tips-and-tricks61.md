---
layout: post
title: "Azure Tips and Tricks Part 61 - Java in Azure Function with VS Code"
excerpt: "Learn how to use Java in Azure Functions with VS Code"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Java in Azure Function with VS Code

I just spent time over the weekend playing with Java in Azure Functions. As a prior Java developer and Azure Functions fan, you'll be happy to know that you can scaffold an app in a couple of ways. 

## Getting setup

You'll need a few things before getting started such as: 

[.NET Core](https://www.microsoft.com/net/core),[JDK](https://www.azul.com/downloads/zulu/), [Azure CLI](https://docs.microsoft.com/cli/azure), [Apache Maven](https://maven.apache.org) and [Node.js](https://nodejs.org/download/). 

 Once that is ready, you can easily turn this on by `npm install -g azure-functions-core-tools@core`. You should see the following: 

```text

> azure-functions-core-tools@2.0.1-beta.18 uninstall /usr/local/lib/node_modules/azure-functions-core-tools
> node lib/uninstall.js

deleting /Users/mbcrump/.azurefunctions/bin
/usr/local/bin/func -> /usr/local/lib/node_modules/azure-functions-core-tools/lib/main.js
/usr/local/bin/azfun -> /usr/local/lib/node_modules/azure-functions-core-tools/lib/main.js
/usr/local/bin/azurefunctions -> /usr/local/lib/node_modules/azure-functions-core-tools/lib/main.js

> azure-functions-core-tools@2.0.1-beta.22 postinstall /usr/local/lib/node_modules/azure-functions-core-tools
> node lib/install.js

[==================] Downloading Azure Functions Cli
+ azure-functions-core-tools@2.0.1-beta.22
added 1 package and updated 6 packages in 18.873s
```

## Use Maven to generate a Java Azure Functions app

You'll now take advantage of Maven and will scaffold a new Azure Functions project with `mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure   -DarchetypeArtifactId=azure-functions-archetype`. 

<img style="border:3px solid #021a40" src="/files/functionjava1.gif">

**Remember this!** There is a ridiculous number of things you can do with Maven. Check out the [GitHub repo](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-functions-maven-plugin) for usage and configuration examples. 
{: .notice--primary}

I'd also recommend installing the extension that is suggested for Java projects:

<img style="border:3px solid #021a40" src="/files/functionjava2.png">

OK, cool! We have scaffolded a Java Azure Function project and we are using VS Code to edit it. 

<img style="border:3px solid #021a40" src="/files/functionjava3.png">

Make note of the following comments in the Java code as we'll use the 2nd curl command shortly:

```text
    /**
     * This function listens at endpoint "/api/hello". Two ways to invoke it using "curl" command in bash:
     * 1. curl -d "HTTP Body" {your host}/api/hello
     * 2. curl {your host}/api/hello?name=HTTP%20Query
     */
```

You can now run `mvn clean package` and `mvn azure-functions:run` from inside the integrated terminal or command prompt. You'll now have a localhost URL that you run the curl command `curl {your host}/api/hello?name=HTTP%20Query` to ensure it was working properly. You should see `Hello HTTP Query!`. 

## Use the plugin for Visual Studio Code 

**Remember this!**  Keep in mind that you'll need all the prerequisites covered earlier in this post before proceeding. 
{: .notice--primary}

I covered the plugin back in [post 50](https://www.michaelcrump.net/azure-tips-and-tricks50/), but basically grab the plugin and login into your Azure account and create a new Azure Function as shown below:

Click New and you'll see the following: 

<img style="border:3px solid #021a40" src="/files/functionjava4.png">

Now you'll walk through the same steps that you did before through the command line, but now right inside VS Code. 

<img style="border:3px solid #021a40" src="/files/functionazure4.gif">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 