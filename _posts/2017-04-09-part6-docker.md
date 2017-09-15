---
layout: post
title: "Day 6 - Exploring Docker for Windows - Accessing Files inside a Container"
excerpt: "Learn how to access the files inside a container in Docker"
tags: [docker, windows, edge, dotnet, dotnetcore, web]
share: true
comments: true
---

## Intro

In this mini-series, I plan to walk you through [Docker](https://www.docker.com) as I learn it. 

A complete list of post in this series is included below :

* [Day 1 - Exploring Docker for Windows - Getting Started](http://michaelcrump.net/part1-docker/)
* [Day 2 - Exploring Docker for Windows - Stopping and Restarting Containers](http://michaelcrump.net/part2-docker/)
* [Day 3 - Exploring Docker for Windows - Removing Containers and Images](http://michaelcrump.net/part3-docker/)
* [Day 4 - Exploring Docker for Windows - Running Docker Documentation Locally](http://michaelcrump.net/part4-docker/)
* [Day 5 - Exploring Docker for Windows - Running A Command Prompt Inside a Container](http://michaelcrump.net/part5-docker/)
* [Day 6 - Exploring Docker for Windows - Accessing Files inside a Container](http://michaelcrump.net/part6-docker/)

## Accessing Files inside a Container

One thing that I'm finding that I need more and more is access to the files inside of a container. There are a lot of great guides on mapping a drive using Windows Explorer and I'd encourage you [read this one](https://rominirani.com/docker-on-windows-mounting-host-directories-d96f3f056a2c) if you are looking for that. If you are like me and using Windows 10 to host and work with Docker, than you might want to use the command-line instead of Windows explorer.  Open up PowerShell and type the following : 

	docker run -it microsoft/dotnet:nanoserver powershell

We are now running PowerShell in a container inside of a PowerShell on our local machine. You can quickly determine which version of PowerShell you are using by listing out a directory as shown below. 

	Windows PowerShell
	Copyright (C) 2016 Microsoft Corporation. All rights reserved.
	
	PS C:\> dir
	    Directory: C:\
	
	Mode                LastWriteTime         Length Name
	----                -------------         ------ ----
	d-----         4/9/2017   8:14 PM                Program Files
	d-----        7/16/2016   5:09 AM                Program Files (x86)
	d-r---        3/20/2017   7:34 AM                Users
	d-----        3/20/2017   7:35 AM                Windows
	-a----       11/20/2016   3:32 AM           1894 License.txt
	
Notice that it has a `License.txt` file. You can use the `type` command to list out its contents and will see it is a host container image licensed by Microsoft. You can navigate to any directory, list out the contents, add or delete a file. 

*Note* : If you are using Windows Server, then you can open Computer Management and see the drive after running the `docker run -it microsoft/dotnet:nanoserver powershell` command. You can simply assign the drive a letter and examine it in File Explorer. Just FYI - I wouldn't do this in a production environment. 

## Environment variables inside a Container

While you are already in PowerShell, you can also grab environment variables by running the following command :

	ls env:\

Which outputs the following : 

	Name                           Value
	----                           -----
	ALLUSERSPROFILE                C:\ProgramData
	APPDATA                        C:\Users\ContainerAdministrator\AppData\Roaming
	CommonProgramFiles             C:\Program Files\Common Files
	CommonProgramFiles(x86)        C:\Program Files (x86)\Common Files
	CommonProgramW6432             C:\Program Files\Common Files
	COMPUTERNAME                   A6F1D1FF8D31
	ComSpec                        C:\Windows\system32\cmd.exe
	DOTNET_SDK_DOWNLOAD_URL        https://dotnetcli.blob.core.windows.net/dotnet/Sdk/1.0.1/dotnet-dev-win-x64.1.0.1.zip
	DOTNET_SDK_VERSION             1.0.1
	LOCALAPPDATA                   C:\Users\ContainerAdministrator\AppData\Local
	NUGET_XMLDOC_MODE              skip
	NUMBER_OF_PROCESSORS           2
	OS                             Windows_NT
	Path                           C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPo...
	PATHEXT                        .COM;.EXE;.BAT;.CMD
	PROCESSOR_ARCHITECTURE         AMD64
	PROCESSOR_IDENTIFIER           Intel64 Family 6 Model 61 Stepping 4, GenuineIntel
	PROCESSOR_LEVEL                6
	PROCESSOR_REVISION             3d04
	ProgramData                    C:\ProgramData
	ProgramFiles                   C:\Program Files
	ProgramFiles(x86)              C:\Program Files (x86)
	ProgramW6432                   C:\Program Files
	PSMODULEPATH                   C:\Users\ContainerAdministrator\Documents\WindowsPowerShell\Modules;C:\Program Files\...
	PUBLIC                         C:\Users\Public
	SystemDrive                    C:
	SystemRoot                     C:\Windows
	TEMP                           C:\Users\ContainerAdministrator\AppData\Local\Temp
	TMP                            C:\Users\ContainerAdministrator\AppData\Local\Temp
	USERDOMAIN                     User Manager
	USERNAME                       ContainerAdministrator
	USERPROFILE                    C:\Users\ContainerAdministrator
	windir                         C:\Windows

This again is an easy way to determine if you are in a container or not and contains other special environment variables such as .NET Core which we looked at in the [last post](http://michaelcrump.net/part5-docker/). 


## Wrap-up

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 
