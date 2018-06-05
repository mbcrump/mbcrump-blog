---
layout: post
title: "Azure Tips and Tricks Part 129 - Using OCR to extract text from images from the Azure Portal"
excerpt: "Learn how to use OCR to extract text from images from the Azure Portal"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Check out Azure.Source by [Rob Caron](https://twitter.com/RobCaronMSFT)** : A very nice mix of Azure news, announcements, videos, podcast and more. [Read weekly](https://azure.microsoft.com/en-us/blog/azure-source-volume-34/)
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Using OCR to extract text from images from the Azure Portal

I recently needed the ability to extract text from an image. I was very cautious as several free alternatives that exist on the web said they may keep the image (and or text). So I did what any developer would do and just rolled my own. But instead of creating an application, I took it upon myself to use the power of the Azure Portal to accomplish this. 

1.) Open the [Azure Portal](www.portal.azure.com) and select Cloud Shell from the top menu. Now change the scripting language from BASH to PowerShell. 

<img style="border:3px solid #021a40" src="/files/powershell1.png">

2.) We now need to install the PowerShell Cognitive Services module. You can do so by typing `Install-Module PSCognitiveservice -Verbose -Force`. Sample output is below:

```powershell
PS Azure:\> Install-Module PSCognitiveservice -Verbose -Force
VERBOSE: Using the provider 'PowerShellGet' for searching packages.
VERBOSE: The -Repository parameter was not specified.  PowerShellGet will use all of the registered repositories.
VERBOSE: Getting the provider object for the PackageManagement Provider 'NuGet'.
VERBOSE: The specified Location is 'https://www.powershellgallery.com/api/v2/' and PackageManagementProvider is 'NuGet'.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='PSCognitiveservice'' for ''.
...
VERBOSE: Module 'pscognitiveservice' was installed successfully to path 'C:\Users\ContainerAdministrator\Documents\WindowsPowerShell\Modules\pscognitiveservice\0.3.5'.
Azure:\
PS Azure:\>
```

3.) Import the module by typing `Import-Module PSCognitiveservice -V` Sample output is below:

```powershell
PS Azure:\> Import-Module PSCognitiveservice -Verbose
VERBOSE: Loading module from path 'C:\Users\ContainerAdministrator\Documents\WindowsPowerShell\Modules\PSCognitiveservice\0.3.5\PSCognitiveservice.psd1'.
VERBOSE: Populating RepositorySourceLocation property for module PSCognitiveservice.
VERBOSE: Loading module from path 'C:\Users\ContainerAdministrator\Documents\WindowsPowerShell\Modules\PSCognitiveservice\0.3.5\PSCognitiveService.psm1'.
VERBOSE: Importing function 'ConvertTo-Thumbnail'.
VERBOSE: Importing function 'Get-Face'.
VERBOSE: Importing function 'Get-ImageAnalysis'.
...
VERBOSE: Importing alias 'analyze'.
VERBOSE: Importing alias 'bing'.
...
VERBOSE: Importing alias 'ocr'.
VERBOSE: Importing alias 'sentiment'.
VERBOSE: Importing alias 'tag'.
VERBOSE: Importing alias 'thumbnail'.
Azure:\
```

4.) Now you'll need to create a cognitive services account. You can do either in the portal (you may already have one) or by typing `New-CognitiveServiceAccount AccountType ComputerVision -Verbose`

Just make sure you select **Free**. 

<img style="border:3px solid #021a40" src="/files/powershell2.png">

5.) Load the configuration into your environment variables with `lcfg -fromAzure -Verbose` Sample output is below:

```powershell
PS Azure:\> lcfg -fromAzure -Verbose
VERBOSE: Testing Azure login
VERBOSE: Logged in.
VERBOSE: Fetching AzureRM Cognitive Service accounts
VERBOSE: 1 Service found in AzureRM [ComputerVision]
VERBOSE: Setting $env:API_SubscriptionKey_ComputerVision for Cognitive Service: ComputerVision
VERBOSE: Setting $env:API_Location_ComputerVision for Cognitive Service: ComputerVision


Name                           Value
----                           -----
ServiceName                    ComputerVision
Location                       westus
SubscriptionKey                yourkey
EndPoint                       https://westus.api.cognitive.microsoft.com/vision/v1.0
```

6.) Type the following line and just replace the **url**

`ocr -URL https://s3-us-west-2.amazonaws.com/i.cdpn.io/10994.zekgx.4df25d8a-eb50-4007-a0df-6ae0aaf87974.png -Verbose | ForEach-Object {$_.regions.lines} | ForEach-Object { $_.words.text -join ' '}`

And you now have your text!

<img style="border:3px solid #021a40" src="/files/powershell3.png">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 