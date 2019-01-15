---
layout: post
title: "Azure Tips and Tricks Part 179 - Using Azure Media Analytics to search for specific terms in a Video"
excerpt: "Learn how to use azure media analytics to search for specific terms in a video"
tags: [azure, media, analytics, tipsandtricks]
share: true
comments: true
---
 
**NEW:** The FREE Azure Developer Guide eBook (Fall 2018 Edition) is now [available!](http://aka.ms/azuredevebook)
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}

## Using Media Analytics to search for specific terms in a Video
 
 Check out [Part 1 - A Lap Around Azure Media Player](https://www.michaelcrump.net/azure-tips-and-tricks178/) if you would like a quick intro before diving in.

Once you start taking advantage of Azure Media Services to deliver audio and video content to your users, you also gain access to an expanding suite of capabilities: [Azure Media Analytics](https://azure.microsoft.com/en-us/services/media-services/media-analytics/?v=18.18). Using artificial intelligence and machine learning technologies, Azure Media Analytics enables a variety of insights and capabilities including indexing, facial and emotion detection, optical character recognition, and time lapsing. 

The quickest way to use Azure Media Analytics is through a SaaS application called [Video Indexer](https://vi.microsoft.com/en-us/). This service is free for 10 hours, after which you can connect it to your Azure Media Services account and assume a [pricing model](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/video-indexer/) dependent on storage and processing speed. Video Indexer includes a number of preprocessed videos, or you can upload your own.

In the sample videos, you can search for terms—like “football”—and get a feel for how the indexing could work for your application needs.
 
<img style="border:3px solid #021a40" src="/files/seahawks-1.png">

If you select [one of the videos](https://www.videoindexer.ai/accounts/00000000-0000-0000-0000-000000000000/videos/4452cf7e59/) from the original sample list, you’ll see even more insights gleaned from that video, including keywords, sentiment analysis, and facial recognition.

<img style="border:3px solid #021a40" src="/files/seahawks-2.png">

While the output is compelling, you might be wondering how to make use of it in the context of your own applications. First, you can [connect Video Indexer with your own Media Services account in Azure](https://docs.microsoft.com/en-us/azure/cognitive-services/video-indexer/connect-to-azure#manual-configuration). Within the Azure portal, you will then have access to the various assets produced by Video Indexer (as well as be able to access its capability there). Below you can clearly see the various outputs of the process including various caption files (with the .vtt, .smi, and .ttml extensions), an audio index file (.aib), and the XML-formatted keywords file.

<img style="border:3px solid #021a40" src="/files/indexer.png">

For [this particular video from Vimeo](https://vimeo.com/255872218), here’s a snippet of the keywords XML showing the extracted keywords, locations in the clip, and confidence rating.   

```xml
<rss version="2.0"  xmlns:mavis="http://www.microsoft.com/dtds/mavis/">
<channel>
  <mavis:keywords>dude crazy running,specific complex handshaking,parallel universe,girls,birthday,kid,month,julian,familiarity,sense,handshake,grabbing,fun,friends,life,friendship,shot</mavis:keywords>
  <items>
    <mavis:keyword Content="dude crazy running" Count="1" AvgConfidence="0.90">
      <mavis:keyworddetail Confidence="0.90" Offset="24.86" />
    </mavis:keyword>
    <mavis:keyword Content="specific complex handshaking" Count="1" AvgConfidence="0.80">
      <mavis:keyworddetail Confidence="0.80" Offset="77.79" />
    </mavis:keyword>
    <mavis:keyword Content="parallel universe" Count="1" AvgConfidence="1.00">
      <mavis:keyworddetail Confidence="1.00" Offset="111.74" />
    </mavis:keyword>
    <mavis:keyword Content="girls" Count="1" AvgConfidence="0.85">
      <mavis:keyworddetail Confidence="0.85" Offset="35.46" />
    </mavis:keyword>
    <mavis:keyword Content="birthday" Count="2" AvgConfidence="0.80">
      <mavis:keyworddetail Confidence="0.61" Offset="36.25" />
      <mavis:keyworddetail Confidence="1.00" Offset="39.48" />
    </mavis:keyword>
   …   
  </items>
</channel>
</rss>
```

In the snippet of XML above, you’ll see that “birthday” appears twice, near the 36 and the 39 second marks. You might use this information to present the user a list of links that take them directly to the portions of the video containing the keyword. If using Video Indexer to play back the video, the `t` query parameter can be used to specify the start time, in seconds:
- `https://www.videoindexer.ai/.../videos/79cf1a52d0/?t=36.25`
- `https://www.videoindexer.ai/.../videos/79cf1a52d0/?t=39.48`

For even more programmatic control, an [underlying API](https://api-portal.videoindexer.ai/) drives the functionality exposed by the Azure portal and the Video Indexer. The key method, [Get Video Index](https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-Video-Index?), returns a JSON document containing all the results of the indexing operations, and other APIs can be used to submit and process videos as well as list and search videos for specific content.

And lastly, from a user experience perspective, the insights widgets and player that you see within the Video Indexer app can be [embedded and customized as part of your own application](https://docs.microsoft.com/en-us/azure/cognitive-services/video-indexer/video-indexer-embed-widgets).

Pretty cool stuff, go check it out!


**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
