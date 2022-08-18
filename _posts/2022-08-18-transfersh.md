---
layout: post
title: "Transfer.sh - Share files from the command line"
excerpt: "Learn how to share files from the command line"
tags: [linux, file sharing, resources]
share: true
comments: true
---
 
## Transfer files from one Linux system to another
 
I recently ran into a situation where I needed to transfer files from a Linux system to a Windows box but didn't have access to create a RDP session or SSH tunnel. I was looking for a solution and remembered that I could use [https://transfer.sh/](https://transfer.sh/) to do it. 

Basically on the Linux system or wherever you have access to cURL, you can run this command `curl --upload-file FILE-TO-UPLOAD https://transfer.sh/FILE-TO-UPLOAD
`

In my case I have a file on my HDD that is named `test.txt` and the contents of it are: 

`Hello from MichaelCrump.net`

When I run `curl --upload-file test.txt https://transfer.sh/test.txt` then the output displays where the file is stored at. In my example, it went to `https://transfer.sh/vSe7c5/test.txt`. I could now visit this site on another computer to download the file. 

How cool is that?!?

There is also a set of other cool features such as:

* Free to use
* You can upload multiple files at once
* You can encrypt your files with gpg before transfer
* wget, python supports
* much more!

Check it out and LMK what you think!

## Do you want more articles like this?
If you'd like to learn more Tips and Tricks, then follow me on [twitter - http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks, just leave a comment below.
