---
layout: post
title: "How can I use MVVM with Xamarin.Forms?"
excerpt: "This screencast walks you through a simple example of using MVVM with Xamarin.Forms."
tags: [visualstudio, dotnet, csharp, xamarin]
link: https://www.youtube.com/watch?v=K_c0Wcd-MCE
share: true
---
## Intro to MVVM

The [Model-View-ViewModel](https://msdn.microsoft.com/en-us/library/Hh848246.aspx) pattern provided a clean separation of concerns between the user interface controls and their logic. Several reasons you would want to implement it are: 

* A clean separation between application logic and the UI will make an application easier to test, maintain, and evolve. 
* Rich data binding and dependency properties provides the means to connect a UI to a View Model.
* It enables a developer-designer workflow. When the UI XAML is not tightly coupled to the code-behind, the designers can work without independently. 
* It increases application testability. Moving the UI logic to a separate class that can be instantiated independently of a UI technology makes unit testing much easier.

It should be no surprise that users of Xamarin will want to use this in their next Xamarin.Forms projects. In this video, I'll show you step-by-step how to use MVVM in a new Xamarin.Forms project. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/K_c0Wcd-MCE" frameborder="0" allowfullscreen></iframe>


## Wrap-up

I hope this clears things up and don't forget to leave comments in the YouTube comment section. Feel free to email me any question that you would like answered at michael@michaelcrump.net. 