---
layout: post
title: A Better way to Access Swift From the Terminal
excerpt: 
tags: 
comments: true
---

###Introduction

In my [original post](http://michaelcrump.net/running-swift-from-the-terminal), I described how to create an alias to run Swift from the terminal. The only problem was when the user closed the terminal window, they would have to run the 'alias' command again. In this short tutorial, we are going to setup a way that the alias "sticks" between terminal sessions. 

###Open the Terminal Window Again
Enter the follow command to open your .bash_profile in TextEdit:

	touch ~/.bash_profile; open ~/.bash_profile
	
Enter the following command in TextEdit changing only the Xcode6-Beta**XX** number (for whichever version of the beta you are using):

	alias swift="/Applications/Xcode6-Beta4.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/swift"
	
Save the File by pressing CMD+S and quit TextEdit by pressing CMD-Q.

Return to the terminal window and type:

	source ~/.bash_profile
	
This will load the bash file without having to reboot. 

Now if you simply type swift then you can access the Swift REPL. 

###After a Reboot

Simply type swift from the terminal without having to set the alias again since it was loaded during startup in your .bash_profile. 

