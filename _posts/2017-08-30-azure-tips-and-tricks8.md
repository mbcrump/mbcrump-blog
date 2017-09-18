---
layout: post
title: "Azure Tips and Tricks Part 8 - Configure the Azure CLI to set Output Defaults and more"
excerpt: "Learn how to configure the Azure CLI"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List

[Click here to view the complete list of Azure Tips and Tricks ](https://www.michaelcrump.net/azure-tips-and-tricks-complete-list/)

## Configure the Azure CLI to set Defaults and More

In my last tip, I covered using the `--output Table` parameter to customize the results from the Azure CLI. You can also set it as a default amongst other thing. Simply run `az configure` and you'll see the following : 

	Your settings can be found at /home/mbcrump/.azure/config
	Your current configuration is as follows:
	
	[cloud]
	name = AzureCloud
	
	[core]
	first_run = yes
	output = table
	collect_telemetry = yes
	
	[logging]
	enable_log_file = no
	
	Do you wish to change your settings? (y/N):

If you press Y, then you'll get an option to change the default output as shown below: 

	What default output format would you like?
	 [1] json - JSON formatted output that most closely matches API responses
	 [2] jsonc - Colored JSON formatted output that most closely matches API responses
	 [3] table - Human-readable output format
	 [4] tsv - Tab and Newline delimited, great for GREP, AWK, etc.

If you make a selection, then you'll see an option to add file logging: 

	Would you like to enable logging to file?

And finally an option to opt into data collection: 

	Microsoft would like to collect anonymous Azure CLI usage data to improve our CLI.  Participation is voluntary and when you choose to participate, your device automatically sends information to Microsoft about how you use Azure CLI.  To update your choice, run "az configure" again.
	Select y to enable data collection. (Y/n):

Here is a sample of setting the configuration and running a command:

<img src="/files/azuretip8.gif">


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 