---
layout: post
title: "Azure Tips and Tricks Part 164 - Defining Parameters to be used with ARM Templates"
excerpt: "Learn how to use provide parameters with ARM templates"
tags: [azure, arm, templates, appsettings]
share: true
comments: true
---

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}

# Azure Tips and Tricks – Copying Application Settings with an ARM Template

* [Part 1](https://www.michaelcrump.net/azure-tips-and-tricks162/)
* [Part 2](https://www.michaelcrump.net/azure-tips-and-tricks163/) 
* [Part 3 - This Post]

## Yesterday on Azure Tips and Tricks

You’ve already seen that you can automate deploying static configuration information like app settings with your ARM template. But what about providing parameters that allows end-users to input values **BEFORE** deployment. That is what we'll learn today!

## Getting Started

Go ahead and search for **Templates** inside the Azure Portal and click **Add** to create a new one.

Enter a **name** and a **description** and on the ARM Template. 

## Fill-in-the-blank settings

We want to have dynamic settings that are customizable every time you deploy your web app instead of having them be the same each time, you just need to add the parameter values for what you want to your ARM template.

Below is a sample of three values (`FirstNameValue`, `LastNameValue` and `SSNValue`) that we previously hard-coded before: 

```json
"FirstNameValue": {
    "type": "string"
},
"LastNameValue": {
    "type": "string"
},
"SSNValue": {
    "type": "string"
},

```

We'll add the same parameters called `FirstNameValue`, `LastNameValue` and `SSNValue` to the parameters collection of the template. From now on, every time you deploy this template, you will be prompted to enter a value for each one.

```json
"siteConfig": {
    "appSettings": [
        {
            "name": "MyFirstName",
            "value": "[parameters('FirstNameValue')]"
        },
        {
            "name": "MyLastName",
            "value": "[parameters('LastNameValue')]"
        },
        {
            "name": "MySSN",
            "value": "[parameters('SSNValue')]"
        }
    ]
}
```

## Putting it all together 

Our full template file looks like the following:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "appServiceName": {
            "type": "string",
            "minLength": 1,
            "maxLength": 10
        },
        "appServicePlanName": {
            "type": "string",
            "minLength": 1
        },
        "FirstNameValue": {
                "type": "string"
            },
            "LastNameValue": {
                "type": "string"
            },
            "SSNValue": {
                "type": "string"
            },
        "appServicePlanSkuName": {
            "type": "string",
            "defaultValue": "S1",
            "allowedValues": [
                "F1",
                "D1",
                "B1",
                "B2",
                "B3",
                "S1",
                "S2",
                "S3",
                "P1",
                "P2",
                "P3",
                "P4"
            ],
            "metadata": {
                "description": "Describes plan's pricing tier and capacity. Check details at https://azure.microsoft.com/en-us/pricing/details/app-service/"
            }
        }
    },
    "variables": {
        "appHostingPlanNameVar": "[concat(parameters('appServicePlanName'),'-apps')]"
    },
    "resources": [
        {
            "name": "[variables('appHostingPlanNameVar')]",
            "type": "Microsoft.Web/serverfarms",
            "location": "[resourceGroup().location]",
            "apiVersion": "2015-08-01",
            "sku": {
                "name": "[parameters('appServicePlanSkuName')]"
            },
            "dependsOn": [],
            "tags": {
                "displayName": "appServicePlan"
            },
            "properties": {
                "name": "[variables('appHostingPlanNameVar')]",
                "numberOfWorkers": 1
            }
        },
        {
            "name": "[parameters('appServiceName')]",
            "type": "Microsoft.Web/sites",
            "location": "[resourceGroup().location]",
            "apiVersion": "2015-08-01",
            "dependsOn": [
                "[resourceId('Microsoft.Web/serverfarms', variables('appHostingPlanNameVar'))]"
            ],
            "tags": {
                "[concat('hidden-related:', resourceId('Microsoft.Web/serverfarms', variables('appHostingPlanNameVar')))]": "Resource",
                "displayName": "webApp"
            },
            "properties": {
                "name": "[parameters('appServiceName')]",
                "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('appHostingPlanNameVar'))]",
                "siteConfig": {
                    "appSettings": [
                        {
                            "name": "MyFirstName",
                            "value": "[parameters('FirstNameValue')]"
                        },
                        {
                            "name": "MyLastName",
                            "value": "[parameters('LastNameValue')]"
                        },
                        {
                            "name": "MySSN",
                            "value": "[parameters('SSNValue')]"
                        }
                    ]
                }
            }
        }
    ],
    "outputs": {}
}
```

If you save the template, then the next time you deploy resources using this ARM template, you will be required to put in a new value for the **First Name**, **Last Name**, and **SSN** that will be used in your application settings.

<img style="border:3px solid #021a40" src="/files/customdeploy3.png">

And after deployment, go and check your **App Settings**. 

<img style="border:3px solid #021a40" src="/files/customdeploy4.png">

I hope this three part series helped!


**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
