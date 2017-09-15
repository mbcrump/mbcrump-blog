---
layout: post
title: "Invert Mouse Scroll Wheel on Win 10"
excerpt: "Invert Mouse Scroll Wheel on Win 10"
tags: [visualstudio, dotnet, csharp, windows, xaml, uwp]
share: true
---

## Intro

If you're using Windows 10 and would like the scroll wheel inverted, then open up PowerShell as an admin and run the following command:


	Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Enum\HID\*\*\Device` Parameters FlipFlopWheel -EA 0 | ForEach-Object { Set-ItemProperty $_.PSPath FlipFlopWheel 1 }

This is particularly useful when you are used to using a Mac and running Windows 10 in bootcamp. I would also suggest opening "Mouse and Touchpad" settings and select "No delay (always on)" for the delay settings under Touchpad. 

![image](/files/touchpadwin10.PNG)

## Like this Post?

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below.