---
layout: post
title: Easily Format a SD Card in OSX to FAT32
excerpt: Easily format your SD card to FAT32 in OSX
tags: blog
comments: true
---

## The Problem

I've been working with the Raspberry Pi 2 and wanted to install [NOOBS](https://www.raspberrypi.org/downloads/) on my SD Card to play with Linux. Unforunately, the SD Card that I had would not format to FAT32. I tried using Disk Utility as well as the offical [SDCard application](https://www.sdcard.org/downloads/formatter_4/eula_mac/index.html) for OSX. Both applications would format the card, but I could not click on it in finder and be able to paste files on it. I found an easy fix that I thought I'd share. 


## The Solution

Begin by running the following command :  

{% highlight text %}
diskutil list
{% endhighlight %}

You will see the following options : 

![image](/files/diskutilcommandline.jpg)

For example, if we wanted to format our SDCard to FAT32 and give it the name of RASPBIAN and it was located on /dev/disk2, then we'd run the following command :

{% highlight text %}
sudo diskutil eraseDisk FAT32 RASPBIAN MBRFormat /dev/disk2
{% endhighlight %}

Here is what the terminal would display:

![image](/files/finaloutputformatsdcard.jpg)

You can tell it worked, by running the diskutil list command again and it should show the SDCard as a DOS_FAT_32 type instead of Windows_FAT_32 shown earlier. 

![image](/files/diskutilfinalversionfat32.jpg)


## Like this Post?

Thanks for reading and I hope this helped you save some time!