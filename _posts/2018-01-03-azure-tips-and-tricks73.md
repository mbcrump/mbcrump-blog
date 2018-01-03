---
layout: post
title: "Azure Tips and Tricks Part 73 - Send Emails through Azure with C# and SendGrid"
excerpt: "Learn how to send emails through Azure with C# and SendGrid"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Want to Contribute?** I'm currently looking for folks who want to contribute to Azure Tips and Tricks. If you are interested, then read [more here](https://github.com/mbcrump/mbcrump-blog/blob/master/contributing/index.md).
{: .notice--info}

**Upcoming Schedule** Azure Tips and Tricks resumes with our normal posting schedule starting next Sunday (1/7).
{: .notice--danger}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Send Emails through Azure with C# and SendGrid

I needed to send an email through Azure and I used C# and SendGrid. In this post, I'll walk through the process. 

Go to the **Azure Portal** and search services for **SendGrid** and create an account as shown below. You'll notice that I used the **Free** account as it is good enough for our test. 

<img style="border:3px solid #021a40" src="/files/sendgrid1.png">

Go to your SendGrid account once provisioned and clicked on **Manage** and it will bring you to https://app.sendgrid.com/. 

<img style="border:3px solid #021a40" src="/files/sendgrid2.png">

You are going to want to grab your API key from your SendGrid dashboard. You can find it under **Settings**, then **API Keys**

<img style="border:3px solid #021a40" src="/files/sendgrid3.png">

Give your API Key a name and then give it **Full Access**. 

<img style="border:3px solid #021a40" src="/files/sendgrid4.png">

**Remember this!** Copy this key somewhere safe as we'll be using it again shortly!
{: .notice--primary}

Now that you have your API Key, open Visual Studio and create a new Console Application. You'll need to add in the **SendGrid NuGet package**. You can do this just by searching for **SendGrid** as shown below:

<img style="border:3px solid #021a40" src="/files/sendgrid5.png">

Now, copy and paste the following C# code into your Console application, simply replacing your API key.

```csharp
    class Program
    {
        static void Main(string[] args)
        {
            Execute().Wait();

        }
        static async Task Execute()
        {
            var client = new SendGridClient("ENTER-YOUR-API-KEY-HERE");
            var msg = new SendGridMessage();

            msg.SetFrom(new EmailAddress("michael@michaelcrump.net", "Azure Tips and Tricks"));

            var recipients = new List<EmailAddress>
                {
                    new EmailAddress("a@gmail.com"),
                    new EmailAddress("b@gmail.com"),
                    new EmailAddress("c@gmail.com")
                };
            msg.AddTos(recipients);

            msg.SetSubject("Mail from Azure and SendGrid");

            msg.AddContent(MimeType.Text, "This is just a simple test message!");
            msg.AddContent(MimeType.Html, "<p>This is just a simple test message!</p>");
            var response = await client.SendEmailAsync(msg);

        }
    }
```

Run the application and success!

<img style="border:3px solid #021a40" src="/files/sendgrid6.png">

The source code can be found [here](https://github.com/mbcrump/sendgrid). 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 