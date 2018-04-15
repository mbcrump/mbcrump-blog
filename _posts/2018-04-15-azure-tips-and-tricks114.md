---
layout: post
title: "Azure Tips and Tricks Part 114 - Send JSON to Azure IoT Hub with C#"
excerpt: "A tutorial on how to quickly send JSON to IoT Hub with C#"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Tips and Tricks Videos are NOW Available!** : Get all the goodness of Azure Tips and Tricks in video form. [Read more about it here](http://www.michaelcrump.net/azure-tips-and-tricks106/)
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Easily Send JSON to IoT Hub with C#

I recently needed to send JSON that an IoT Hub could receive and display on an AZ3166 device. Once the AZ3166 device receives the message, then it could do a number of things with the data such as open an door. 

Part 1: 

* Create an IoT Hub and provision the MX Chip (AZ3166) as a device. While we could go into the Azure Portal and create a new IoT Hub and walk through the setup of our device, etc. There is an easier way. 
* [Download the tools](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started#prepare-the-development-environment)
* Open **VS Code**, look under **Arduino Examples** and open the **GetStarted** sample and run `task cloud-provision` in the VS Code terminal..

<img style="border:3px solid #021a40" src="/files/aziothub1.png"/>

* If you switch over to the Azure Portal, and look under your new IoT, then Devices - you should see your new device. 

<img style="border:3px solid #021a40" src="/files/aziothub2.png"/>


Part 2:

* I took the code from the “GetStarted” sample found in VS Code and tweaked the `Screen.print(0, "Unlock Door");` lines in the `GetStarted.ino` file in the `Setup` method. 
* Now on my deivce it prints the “Unlock Door” message in fancy yellow and displays the IP Address and waits for a message to be sent to IoT Hub.

<img style="border:3px solid #021a40" src="/files/aziothub3.png"/>

Part 3:

* Open Visual Studio and create a console application. 
* Add NuGet package : Microsoft.Azure.Devices (Service SDK for Azure IoT Hub)
* I hardcoded my connection string (found in IoT Hub) and mocked the JSON data. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.Azure.Devices;

namespace SendMessageToIoTHub
{
    class Program
    {
        static ServiceClient serviceClient;
        static string connectionString = "mykey";

        static void Main(string[] args)

        {
            serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
            SendCloudToDeviceMessageAsync().Wait();
            Console.ReadLine();
        }

        private async static Task SendCloudToDeviceMessageAsync()
        {
            string mockedJsonData =

                "{ \"Locked\":true}";

            var commandMessage = new Message(Encoding.ASCII.GetBytes(mockedJsonData));
            await serviceClient.SendAsync("AZ3166", commandMessage);
        }
    }
}
```

Part 4:

* The MX Board receives the message from IoT Hub
* It prints the JSON message from the serviceClient code above to the board display. 

<img style="border:3px solid #021a40" src="/files/aziothub4.png"/>

Success! We could evolve this to toggle LEDs, deserialize the JSON, log the message, etc. The sky is the limit.  


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 