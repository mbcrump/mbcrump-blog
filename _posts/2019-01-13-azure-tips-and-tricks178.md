---
layout: post
title: "Azure Tips and Tricks Part 178 - A Lap Around Azure Media Player"
excerpt: "Learn how to use azure media player"
tags: [azure, app service, portal, resources]
share: true
comments: true
---
 
**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}


## Happy New Year!
 
Happy New Year! I hope you all enjoyed your break and are ready to hit the ground running in 2019! As I've spent some of my break exploring video tutorials, I decided to start the new year with Azure Media Player. So, welcome back to Azure Tips and Tricks 2019 Edition!

## A Lap Around Azure Media Player

More and more, video has become an integral part of immersive, modern applications, and with the Azure Media Player your applications can easily surface audio and video content—hosted in Azure Media Services—in the format best for the current viewing device. 

A quick way to get started is to take a look at the [Azure Media Player demo](https://ampdemo.azureedge.net/azuremediaplayer.html), which you can use to experiment with tracks in your own Azure Media Services account or just play back one of the two dozen hosted samples.

<img style="border:3px solid #021a40" src="/files/amp.png">

Just by perusing the samples you get an idea of the variety of adaptive streaming formats and DRM technologies supported. If you look under the “Chosen Player Options” in the left sidebar, you can see what format and playback technology has been selected for your current device. Here DASH stands for Dynamic Adaptive Streaming over HTTP, an international standard for adaptive bitrate streaming.  

However, when playing on an iPhone using Safari, for example, notice that the Azure Media Player opts for the HTTP Live Streaming (HLS) option using native HTML5. For older platforms, Adobe Flash or Microsoft Silverlight might even be selected. Consult the [compatibility matrix](http://amp.azure.net/libs/amp/latest/docs/index.html#compatibility-matrix) to get a better understanding of how the *default* rendering options differ among various browser and platform combinations.

<img style="border:3px solid #021a40" src="./files/amp-ios.jpg">

Media geeks out there will also be interested in the various diagnostics that can be captured as the video is playing. If you suspect your media will be playing in environments with limited bandwidth, you could simulate a throttled network with Chrome’s Developer Tools or another utility and visualize the effect on bitrates and buffering.

<img style="border:3px solid #021a40" src="/files/amp-diag.png">

Embedding the player into your own web application is simple and can be done via an IFrame or, optionally, using the HTML5 video tag with some JavaScript to customize behavior. The Code tab of the Azure Media Player Demo app provides both approaches.  For the IFrame option, you can paste the tag into the \<body\> of a bare bones HTML document and quickly view the result. The HTML5/JavaScript option provides a bit of HTML markup as well as ancillary script (that you would generally save separately and refer to in a \<script\> tag). Below is the JavaScript snippet provided for our sample video
```javascript
var myOptions = {
	nativeControlsForTouch: false,
	controls: true,
	autoplay: true,
	width: "640",
	height: "400",
}
myPlayer = amp("azuremediaplayer", myOptions);
myPlayer.src([
        {
                "src": "https://amssamples.streaming.mediaservices.windows.net/830584f8-f0c8-4e41-968b-6538b9380aa5/TearsOfSteelTeaser.ism/manifest",
                "type": "application/vnd.ms-sstr+xml",
                "protectionInfo": [
                        {
                                "type": "AES",
                                "authenticationToken": "<redacted token>"
                        }
                ]
        }
]);
```


Note that the `amp` object has a number of [options](https://amp.azure.net/libs/amp/latest/docs/index.html#options) that can be used to customize the capabilities of the player, including whether controls should be displayed, options for playback speed, [live captioning](https://amp.azure.net/libs/amp/latest/samples/dynamic_webvtt.html), and hot keys for controlling the volume, screen size, and play position. Programmatically, you can tap into [events](https://amp.azure.net/libs/amp/latest/docs/index.html#amp.eventname) just as you would expect for any JavaScript object. There is even a [plug-in model](http://amp.azure.net/libs/amp/latest/docs/PLUGINS.html) through which you and other developers can enhance player functionality.

For more details on specific capabilities, as well as code for a variety of scenarios, be sure to check out the latest [docs](http://amp.azure.net/libs/amp/latest/docs/index.html) and particularly [these samples](http://amp.azure.net/libs/amp/latest/docs/samples.html), which show how to exercise more of the player options themselves like playback speed, localization of captions, and event handling.

Come back tomorrow and we'll talk about Azure Media Analytics. 

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
