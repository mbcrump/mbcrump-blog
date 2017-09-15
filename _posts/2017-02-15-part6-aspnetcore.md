---
layout: post
title: "Day 6 - Migrating an existing .NET Core to csproj"
excerpt: "Learn how to create migrate an existing .NET Core app to csproj"
tags: [edge, windows, chrome, aspnet, dotnetcore, uwp]
share: true
comments: true
---

Disclaimer: *I am **not** on the .NET Core Team*. I used the tools available publicly and have no insights into the future of .NET Core. It looks very bright though. :)

The working source code for this project can be found [here](https://github.com/mbcrump/DotNetCorePlayground). 


## Intro

A complete list of post in this series is included below :

* [Day 1 - Installing and Running .NET Core on a Windows Box](http://michaelcrump.net/getting-started-with-aspnetcore/)
* [Day 2 - Taking a Look at the Visual Studio Templates for .NET Core](http://michaelcrump.net/part2-aspnetcore/)
* [Day 3 - Running a .NET Core app on a Mac](http://michaelcrump.net/part3-aspnetcore/)
* [Day 4 - Creating a NuGet Package from .NET Core app](http://michaelcrump.net/part4-aspnetcore/)
* [Day 5 - Creating a Test Project from .NET Core](http://michaelcrump.net/part5-aspnetcore/)
* [Day 6 - Migrating an existing .NET Core to csproj](http://michaelcrump.net/part6-aspnetcore/)
* [Day 7 - Creating an ASP.NET Core Web Application](http://michaelcrump.net/part7-aspnetcore/)
* [Day 8 - Using Visual Studio Code with a .NET Core Console Application](http://michaelcrump.net/part8-aspnetcore/)
* [Day 9 - Creating a .NET Core Console App inside of Visual Studio Code](http://michaelcrump.net/part9-aspnetcore/)
* [Day 10 - Using JetBrains Rider with a .NET Core Console Application](http://michaelcrump.net/part10-aspnetcore/)

In this post, we're going to look at how to migrate an existing .NET Core app to MSBuild.

## But first, the why?

Remember when we created a new .NET Core Console app and examined the contents what we found? That's right, two files : 

* Program.cs
* project.json

When we start to look at the [roadmap](https://github.com/dotnet/core/blob/master/roadmap.md) of .NET Core, we will quickly see that MSBuild is replacing project.json. In fact if you create a new .NET Core app using the MSBuild template (available with the latest preview), you will see the following files : 

* Program.cs
* msbuild.csproj

The key takeaway here is that you may have .NET Core apps that use `project.json` that you might want to replace with `msbuild.csproj` in the future. This is what I intend to talk about today. 

## Installing the latest SDK

Before we begin, make sure you have the app found [here](https://github.com/mbcrump/DotNetCorePlayground) if you want to follow along. 

We are going to begin by downloading the latest SDK. Start by heading out to the [GitHub repo](https://github.com/dotnet/cli) and downloading the file located below.

![image](/files/installerbinarycore.png)

Go ahead and run through the installer and make sure you close the command prompt and open it back up if it was already open. 

Now run the command `dotnet --info` and you should see the following (or higher depending on when you read this blog post)

	Product Information:
	 Version:            1.0.0-rc4-004828
	 Commit SHA-1 hash:  58b6a0810f
	
	Runtime Environment:
	 OS Name:     Windows
	 OS Version:  10.0.14393
	 OS Platform: Windows
	 RID:         win10-x64
	 Base Path:   C:\Program Files\dotnet\sdk\1.0.0-rc4-004828

If that is what you have, then it is OK to move forward.  

## Taking a quick look at the commands

After installing the new bits, if you run `dotnet help` then you will see a couple of new commands. Here is a full list: 

	Commands:
	  new           Initialize .NET projects.
	  restore       Restore dependencies specified in the .NET project.
	  build         Builds a .NET project.
	  publish       Publishes a .NET project for deployment (including the runtime).
	  run           Compiles and immediately executes a .NET project.
	  test          Runs unit tests using the test runner specified in the project.
	  pack          Creates a NuGet package.
	  migrate       Migrates a project.json based project to a msbuild based project.
	  clean         Clean build output(s).
	  sln           Modify solution (SLN) files.

The one that we're interested in is `migrate`. 

Tip: If you ever want to look at the commands in the source code, then check out this [page](https://github.com/dotnet/cli/blob/2d93968a88a724ec69a3c3cfd0ad92576101cbfe/src/dotnet/Program.cs). 

## Using dotnet migrate

Begin by running `dotnet help migrate`
	
	Arguments:
	  <PROJECT_JSON/GLOBAL_JSON/SOLUTION_FILE/PROJECT_DIR>  The path to one of the following:
	    - a project.json file to migrate.
	    - a global.json file, it will migrate the folders specified in global.json.
	    - a solution.sln file, it will migrate the projects referenced in the solution.
	    - a directory to migrate, it will recursively search for project.json files to migrate.
	Defaults to current directory if nothing is specified.

You will see a couple of options, we are just going to navigate inside the proper directory and run the `dotnet migrate` command. It will output the following : 

	Project NetCoreConsoleApp migration succeeded (C:\Users\mbcrump\Documents\Visual Studio 2015\Projects\NetCoreConsoleApp\src\NetCoreConsoleApp).
	Summary
	Total Projects: 1
	Succeeded Projects: 1
	Failed Projects: 0
	
	The project migration has finished. Please visit https://aka.ms/coremigration to report any issues you've encountered or ask for help.
	Files backed up to C:\Users\mbcrump\Documents\Visual Studio 2015\Projects\NetCoreConsoleApp\src\NetCoreConsoleApp\backup\

We see that the project succeeded and it created a backup folder which contains our `.xproj` and `.json` files. 

So what do we have now in our directory? 

If we type `dir` then we will see a new .csproj file as shown below : 

	02/15/2017  06:58 PM    <DIR>          .
	02/15/2017  06:58 PM    <DIR>          ..
	02/07/2017  04:59 PM               314 Account.cs
	02/15/2017  06:58 PM    <DIR>          backup
	02/13/2017  06:31 PM    <DIR>          bin
	02/15/2017  06:58 PM               887 NetCoreConsoleApp.csproj
	02/07/2017  04:41 PM    <DIR>          obj
	02/08/2017  07:04 PM             1,094 Program.cs
	02/07/2017  04:10 PM    <DIR>          Properties
	               3 File(s)          2,295 bytes
	               6 Dir(s)   53,236,098,048 bytes free

## Back to Visual Studio

If you try to open the project in Visual Studio 2015 then you will see the following error:

![image](/files/errordotnetcorevs.png)

This cryptic error just means that VS 2015 is not supported. If you want to open this project then you will need to install the [Visual Studio 2017 release candidate](https://www.visualstudio.com/). 

Once that is resolved you should be good to go! 

## Wrap-up

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 