---
layout: post
title: "Azure Tips and Tricks Part 163 - Provide Static App Settings Values to an ARM Template"
excerpt: "Learn how to use provide static values to ARM templates"
tags: [azure, arm, templates, appsettings]
share: true
comments: true
---

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}

# Azure Tips and Tricks – Copying Application Settings with an ARM Template

[Part 1](https://www.michaelcrump.net/azure-tips-and-tricks162/) | [Part 2 - This Post](https://www.michaelcrump.net/azure-tips-and-tricks163/)  | [Part 3 - Coming soon]()

## Yesterday on Azure Tips and Tricks

Building on my previous Azure Tips and Tricks post about what ARM templates are and why you should care, I wanted to give you a quick recipe for a common development task. You’ve already seen that you can automate deploying a web app (and many other resources), but can you also copy configuration information like app settings with your ARM template? Yes! 

## Getting Started

Go ahead and create a resource inside the Azure Portal for a Web App.

Enter a name and a resource group for your web app and click **Automation options** in order to start creating your ARM template.

<img style="border:3px solid #021a40" src="/files/arm_template.png">

As you can see, your template is JSON with multiple values describing how your web app is going to be deployed.

### Static App Settings for your Azure App Service

To make things as easy as possible, let’s assume for now that you want to add the exact same settings every time you deploy your web app template. 

Go to **Deploy** then **Edit Template** and paste the following settings fragment overwriting your template’s resource section. (You could, of course, add as many keys as your web app needs.)

```
  "resources": [
  {
    "apiVersion": "2016-03-01",
    "name": "[parameters('name')]",
    "type": "Microsoft.Web/sites",
    "properties": {
        "name": "[parameters('name')]",
        "siteConfig": {
            "appSettings": [
            {
              "name": "MyFirstName",
              "value": "Michael"
            },
            {
              "name": "MyLastName",
              "value": "Crump"
            },
            {
              "name": "MySSN",
              "value": "355-643-3356"
            }
          ]
        },
        "serverFarmId": "[concat('/subscriptions/', parameters('subscriptionId'),'/resourcegroups/', parameters('serverFarmResourceGroup'), '/providers/Microsoft.Web/serverfarms/', parameters('hostingPlanName'))]",
        "hostingEnvironment": "[parameters('hostingEnvironment')]"
    },
    "location": "[parameters('location')]"
  }],
```

Press **Save** and ensure the **Basic** and **Settings** is filled out. Agree to the terms and check the **Purchase** option. 

<img style="border:3px solid #021a40" src="/files/customdeployment.png">

Note: If it says failure to deploy, then give it a shot again. I have had this happened but maybe it is only happening since I use the Preview. 
{: .notice--primary}

<img style="border:3px solid #021a40" src="/files/create_resource1.png">

 Your app settings will now be deployed with your web app. Save your template and keep it in the freezer until you need to pull it out again.

After deployment, navigate to your **App Service** and go to **Application Settings** and you'll see your site deployed  with the settings we specified earlier. 

<img style="border:3px solid #021a40" src="/files/create_resource1.png">

Come back tomorrow and we'll take a look at adding parameters

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
