---
layout: post
title: "Day 12 - Turning off Telemetry Data in .NET Core"
excerpt: "Learn how to quickly turn off telemetry data in .NET Core"
tags: [edge, windows, chrome, aspnet, dotnetcore, web]
share: true
comments: true
---

## Intro

In this post, we're going to look at how to quickly turn off telemetry data in .NET Core.

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
* [Day 11 - Exploring .NET Core with Visual Studio 2017 and the updated CLI Tools](http://michaelcrump.net/part11-aspnetcore/)

## A word about telemetry data

We all know that telemetry data (or some sort of data) is needed in order to improve a product. You could argue however, that telemetry data should be an opt-in process and I'd agree with you. I like Yeoman's approach to this. The key here is the Yes/No prompt that forces the user to make a decision. 

	==========================================================================
	We're constantly looking for ways to make yeoman better! 
	May we anonymously report usage statistics to improve the tool over time? 
	More info: https://github.com/yeoman/insight & http://yeoman.io
	==========================================================================Y/n

The default behavior of .NET Core is to opt you in, but it displays a whole section relating to the topic as shown below with a way to quickly opt-out. 

	C:\Users\Michael Crump>dotnet --info
	
	Welcome to .NET Core!
	---------------------
	Learn more about .NET Core @ https://aka.ms/dotnet-docs. Use dotnet --help to see available commands or go to https://aka.ms/dotnet-cli-docs.
	
	Telemetry
	--------------
	The .NET Core tools collect usage data in order to improve your experience. The data is anonymous and does not include command-line arguments. The data is collected by Microsoft and shared with the community.
	You can opt out of telemetry by setting a DOTNET_CLI_TELEMETRY_OPTOUT environment variable to 1 using your favorite shell.
	You can read more about .NET Core tools telemetry @ https://aka.ms/dotnet-cli-telemetry.
	
	Configuring...
	-------------------
	A command is running to initially populate your local package cache, to improve restore speed and enable offline access. This command will take up to a minute to complete and will only happen once.
	Decompressing 100% 5445 ms
	Expanding 100% 51482 ms

.NET Core also [outlines](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/telemetry) exactly the data they are collecting which is needed in order to approve the technology being used in many businesses. 

The point that I'm trying to make here is that **a)** data is needed in order to make a product great **b)** be up front that you are collecting telemetry data **c)** if you make a tool that collects telemetry, try to make it very easy for someone to opt-out **d)** provide clear guidance about what data you are collecting. I'm sure there are more things to add to this list, but this is the first that comes to my mind with this topic. 

## Turning it off on Windows

You can quickly turn it off on Windows, by running the `set DOTNET_CLI_TELEMETRY_OPTOUT=1` from a command prompt. After running the command, you can simply run type `SET` to see the current environment variables that Windows has set. Below is a snippet of running the command on my machine. You'll see the OUPOUT value close to the bottom of the list. 

	C:\Users\Michael Crump>SET
	ALLUSERSPROFILE=C:\ProgramData
	APPDATA=C:\Users\Michael Crump\AppData\Roaming
	AppsRoot=D
	AWE_DIR=C:\Program Files (x86)\Khrona LLC\Awesomium SDK\1.6.6\
	CommonProgramFiles=C:\Program Files\Common Files
	CommonProgramFiles(x86)=C:\Program Files (x86)\Common Files
	CommonProgramW6432=C:\Program Files\Common Files
	ComSpec=C:\Windows\system32\cmd.exe
	DOTNET_CLI_TELEMETRY_OPTOUT=1
	HOMEDRIVE=C:
	HOMEPATH=\Users\Michael Crump

## Turning it off on MacOS and Linux

You can also turn it off on MacOS and Linux by running the `export DOTNET_CLI_TELEMETRY_OPTOUT=1` from the shell. 

## Wrap-up

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 