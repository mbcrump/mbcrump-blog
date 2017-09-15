---
layout: post
title: Create a bootable Windows 10 ISO for the Spectre x360 
excerpt: The easiest way that I've found to install Windows 10 on my Spectre x360
tags: blog
comments: true
---

## Intro


If you were an attendee at [Build 2015](http://www.buildwindows.com/), then you walked away with a [HP Spectre x360](http://store.hp.com/webapp/wcs/stores/servlet/us/en/mdp/Laptops/spectre-x360-211501--1) machine. While it may not be powerful enough to be your main machine, it definitely is great for travel, etc. I decided early on that I didn't want any of the software or Windows 8.1 that comes pre-installed on the machine, so here is the steps that I took to remove everything and do a fresh install of the latest Windows 10 preview. 

## Create a Bootable USB Drive

I used an old Lexar 8 GB USB thumb-drive that I had. These can be purchased at Target for around $8 USD. Begin by download the latest [Windows 10 Preview ISO](http://windows.microsoft.com/en-us/windows/preview-iso) and installing [Rufus](http://rufus.akeo.ie/). Launch Rufus and leave all the settings as default, except select the ISO image besides the "Create a bootable disk using" option. It should look like the following : 

![image](/files/rufusandwin10.png)

## Enter Bios

Plug in the laptop, then head straight into BIOS. I didn't even boot into Windows 8.1 and did the following:

* Hit **F10** upon boot to enter BIOS settings and I disabled a majority of the security features and change the boot order to my USB Drive. 
* Upon reboot, hit **F9** and select your USB thumb-drive. (in case it didn't recognize your thumb-drive from the previous step)
* Once Windows 10 boots from the USB thumb-drive, then I deleted all the HP partitions  (leaving only one) and installed Windows 10 from there. 


## After Windows 10 is Installed

I immediately went out to the HP site and [updated the firmware and trackpad drivers](http://support.hp.com/us-en/drivers/selfservice/HP-Spectre-x360-Convertible-PC-Series/7527520/model/7791778#Z7_3054ICK0KGTE30AQO5O3KA30R1). Everything else seemed to just work. 

## Wrap-Up

Now that your machine is setup and you have a bootable ISO, when the final version of Windows 10 comes out, you will be ready! Anyways, thanks for reading and I hope this was the most straight-forward way of getting your machine ready for this awesome OS that is coming out shortly. 

