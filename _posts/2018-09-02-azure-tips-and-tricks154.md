---
layout: post
title: "Azure Tips and Tricks Part 154 - How to quickly check the EndPoint API of QnA Maker"
excerpt: "Learn how to quickly test the QnA Maker knowledge base with Fiddler"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## How to quickly check the EndPoint API of QnA Maker

If you haven't experimented with [QnA Maker](https://qnamaker.ai/) then it is time. It enables you to quickly create a question and answer service from content like FAQ documents, URLs, and product manuals. You can create a knowledge base with existing data sources that you already have. Once complete, you might want to consume the endpoint API through applications such as Fiddler or cURL. In this post, I'll show you quickly how you can do both. 

For Fiddler:

You need to specify `TLS1.2`. Simply go to **Tools** > **Options** > **HTTPS** to make **tls1.2** allowable.

<img style="border:3px solid #021a40" src="/files/fiddlerazure1.png">

For cURL:

Simply replace placeholder text and it should work!

```text
curl \
--header "Content-type: application/json" \
--header "Authorization: EndpointKey placeholder-text-remove-me" \
--request POST \
--data '{"question":"Have you completed the Azure Tips and Tricks Survey yet?"}' \
https://myazureresourcename.azurewebsites.net/qnamaker/knowledgebases/placeholder-text-remove-me/generateAnswer
```

I hope this helped!

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 