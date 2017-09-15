---
layout: post
title: "Pop a Toast Notification in WPF using Win 10 APIs"
excerpt: "Learn how to pop a toast notification in WPF using Win 10 APIs"
tags: [wpf, csharp, xaml, uwp]
share: true
comments: true
---

## Intro

I needed a quick way to pop a Toast Notification in a WPF app using Win 10 APIs. I started by taking a look at this [sample](https://code.msdn.microsoft.com/windowsdesktop/sending-toast-notifications-71e230a2) and decided to strip away some unnecessary code that I didn't need. I landed with [this version](https://github.com/mbcrump/DesktopToast) which doesn't subscribe to the ToastActivated, ToastDismissed or ToastFailed event handlers. Keep in mind that you'll need to add references to the following files if creating this from scratch:

* Browse and find the following file: C:\Program Files (x86)\Windows Kits\10\UnionMetadata\winmd. Add it to your project as a reference. Note: You will need to change the filter to “All Files”.
* Browse and find the directory “C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETCore\v4.5”. Add System.WindowsRuntime.dll to your project.

That's it. 

Here is a demo of it in action. 

![image](/files/toast.gif)


## Wrap-up

Again, this is something that I needed and decided I'd share. In case you haven't noticed, I've started blogging about things that I'm interested in or working on. I've recently wrote 3 other blog posts : 

* [Open UWP apps through Edge or a Web Browser Link](http://michaelcrump.net/open-edge-from-chrome-link/)
* [Calling Windows 10 APIs From a Desktop Application](https://blogs.windows.com/buildingapps/2017/01/25/calling-windows-10-apis-desktop-application/)
* [Command Line Fun for Windows 10 Users](http://michaelcrump.net/command-line-fun-for-win10/)

Be sure to check them out and if you use Twitter, then [I'm on there](http://www.twitter.com/mbcrump) as well.  As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below.