---
layout: post
title: "How do I disable C# 6 Support in Visual Studio 2015?"
excerpt: "It is easier than you think."
tags: [visualstudio, dotnet, csharp]
link: https://www.youtube.com/watch?v=s5jWIzX-uMM
share: true
---
## Intro

Some developers are not yet ready to take the plunge to C# 6, whereas others would like to play with C# 6 without installing Visual Studio 2015. In this episode, I address both issues. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/s5jWIzX-uMM" frameborder="0" allowfullscreen></iframe>

## For those looking for a quick breakdown: 

**How do I disable C# 6 Support in Visual Studio 2015?**

Question: We've already internally adopted Visual Studio 2015 for some of the new features that it has, but we don't want to use C# 6 just yet. Can we disable C# 6, so that our contract developers can open the project in Visual Studio 2013 without any problems and prevent them from using any of the new C# 6 features? 

Answer: You can set the language feature for each project separately by going to Properties => Build tab => Language Version and set your preferred version. From here, you can switch it to whatever C# version you would like. (ex. C# 5.0)

**How do I explore C# 6 features without installing Visual Studio 2015?**

As described in the video, you can use [tryroslyn.azurewebsites.net](http://tryroslyn.azurewebsites.net/). This is what I used for testing new C# 6 features as Visual Studio 2015 was being built.  

## Wrap-up

I hope this clears things up and don't forget to email me any question that you would like answered at michael@michaelcrump.net. 