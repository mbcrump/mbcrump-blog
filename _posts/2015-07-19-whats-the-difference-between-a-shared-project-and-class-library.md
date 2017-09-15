---
layout: post
title: "What is the difference between a Shared Project vs. Class Library?"
excerpt: "I take a look at Shared Projects and Class Libraries in VS 2015"
tags: [visualstudio, dotnet, csharp]
link: https://www.youtube.com/watch?v=ScrRu6Kbr-8
share: true
---
## Intro

I've noticed lots of questions from the developer community with the release of "Shared Projects" inside of Visual Studio 2015. In this video, I aim to clear up any confusion regarding "Shared Projects" vs. Class Libraries. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/ScrRu6Kbr-8" frameborder="0" allowfullscreen></iframe>

## For those looking for a quick breakdown: 

* A class library is compiled and the unit of reuse is the assembly. 

* In a Shared Project, the unit of reuse is the source code and the shared code is incorporated into each assembly that references the shared project. 

Another way of looking at this is, class libraries allow you to reuse C# code, whereas Shared Projects allow you to reuse C# code, XAML files, JavaScript files, etc. 

I hope this clears things up and don't forget to email me any question that you would like answered at michael@michaelcrump.net. 