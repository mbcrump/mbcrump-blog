---
layout: post
title: "Open UWP apps through Edge or a Web Browser Link"
excerpt: "Learn how to open UWP apps through Edge or a web browser link"
tags: [edge, windows, chrome, uwp]
share: true
comments: true
---

## Intro

If you've ever wanted an option to run UWP apps from Edge or through a link in another browser then I have some info for you. There is a vast variety of protocols that you can use if you're on Windows 10. I'll cover a few in this post and show you where you can find more.    

## Through MS Edge

If you open MS Edge and type calculator:// then it will launch the calculator app. You can see my web history already remembers that I typed it before. 

![image](/files/uwpcalculator.png)

The idea is that you can open an app and pass some parameters to it. Take for example the Windows Store. Here we call the Windows Store and pass in Minecraft:

	ms-windows-store://search/?query=Minecraft

![image](/files/minecraftuwp.png)

You can also call other UWP apps like: 

	xbox://
	bingweather://
	ms-clock://

You can find more by open the registry and searching for "URL:" as shown below:

![image](/files/registryuwp.png)

## Through a Hyperlink

You can also make a UWP app launch through a web browser. I'm going to use Chrome in this sample to open MS Edge. All you need to do is simply add the following HTML to your page and obviously replace the URL to whatever site that you'd like to load. 

	<a href="microsoft-edge:http://www.michaelcrump.net">My site</a>

If someone visits your page and click on the above link then it will display the following: 

![image](/files/edgeinchrome.png)

They can click the open button and it will open a new Edge instance or they can cancel out. 

This also works with the other protocols that I mentioned earlier. It will also display a prompt unless your user is using MS Edge. 


## Wrap-up

I needed this functionality for a project that I was working on and thought I'd share. As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below.