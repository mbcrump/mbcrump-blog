---
layout: post
title: "Azure Tips and Tricks Part 175 - Machine Learning with ML.NET and Azure Functions - Part 2 of 2"
excerpt: "In part 1 of this post on ML.NET and Azure Functions, you created a machine learning model with ML.NET that categorizes irises. You also set up a serverless architecture environment with Azure Functions and uploaded your model to it. In this post, you’re going to finish by building an app that uses your machine learning model."
tags: [azure, ML.NET, Azure Functions, Machine Learning, AI]
share: true
comments: true
---

**ATTENTION:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now! No registration required. 
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}

## Azure Tips and Tricks Part 175 - Machine Learning with ML.NET and  Azure Functions - Part 2 of 2


## Intro

 Machine learning can be tricky. Fortunately, Azure is coming up with ways to make it easier for developers to jump into machine learning. In part 1 of this post on ML.NET and Azure Functions, you created a machine learning model with [ML.NET](https://www.microsoft.com/net/apps/machinelearning-ai/ml-dotnet)  that categorizes irises. You also set up a serverless architecture environment with Azure Functions and uploaded your model to it. In this post, you’re going to finish by building an app that uses your machine learning model.

## Identify irisis like a Machine

 This is [part 2](https://www.michaelcrump.net/azure-tips-and-tricks175/) of a two part post on ML.NET inspired by Luis Quintanilla’s [article](http://luisquintanilla.me/2018/08/21/serverless-machine-learning-mlnet-azure-functions/) about using ML.NET with Azure Functions, where he took these two great ideas and combined them. Picking up [with Part 1](https://www.michaelcrump.net/azure-tips-and-tricks145/), you are going to create a new Azure Function project using Visual Studio.

 Note: Make sure you have the Azure Workload installed to see this template. 

 <img style="border:3px solid #021a40" src="/files/azurefunction.png">

Open up the **demo** solution from part 1 in Visual Studio and create a new project using the Azure Functions project template called **serverless_ai**.

 <img style="border:3px solid #021a40" src="/files/httptrigger.png">

 When prompted, select the **Http trigger** option and connect it to your Azure storage account for the project (**mlnetdemostorage1** for this post). Then complete the following steps:
 •	Use NuGet to add the **Microsoft.ML** package to your project.
 •	Copy the **IrisData.cs** and **IrisPrediction.cs** files from your model project to the _serverless_ai_ project. You’ll need them both again.

 Change the name of the Http trigger class _Function1_ to _Predict_ and copy in the following code:

 ```csharp
 using Newtonsoft.Json;
 using Microsoft.ML;

 namespace serverless_ai
 {
     public static class Predict
     {
         [FunctionName("Predict")]
         public static IActionResult Run([HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)]HttpRequest req,
         [Blob("models/model.zip", FileAccess.Read, Connection = "AzureWebJobsStorage")] Stream serializedModel,
         TraceWriter log)
         {
             if (typeof(Microsoft.ML.Runtime.Data.LoadTransform) == null ||
                 typeof(Microsoft.ML.Runtime.Learners.LinearClassificationTrainer) == null ||
                 typeof(Microsoft.ML.Runtime.Internal.CpuMath.SseUtils) == null ||
                 typeof(Microsoft.ML.Runtime.FastTree.FastTree) == null)
             {
                 log.Error("Error loading ML.NET");
                 return new StatusCodeResult(500);
             }

             //Read incoming request body
             string requestBody = new StreamReader(req.Body).ReadToEnd();

             log.Info(requestBody);

             //Bind request body to IrisData object
             IrisData data = JsonConvert.DeserializeObject<IrisData>(requestBody);

             //Load prediction model
             var model = PredictionModel.ReadAsync<IrisData, IrisPrediction>(serializedModel).Result;

             //Make prediction
             IrisPrediction prediction = model.Predict(data);

             //Return prediction
             return (IActionResult)new OkObjectResult(prediction.PredictedLabels);
         }
     }
 }
 ```
 These lines use your model to evaluate new iris data to make a prediction. Your app is ready for testing.

## Test locally before deploying

To test the Azure Function app on your local machine, check your **local.settings.json** file to make sure that **AzureWebJobsStorage** has a value associated with it. This is how your local app will find your uploaded model on your Azure storage account. If this has a value (and it should if you bound the project to your account when you created it), you can just _F5_ the _serverless_ai_ project in order to run it.
Now open up [Postman](https://www.getpostman.com/apps)  (or a similar REST API tool) and send a POST call to http://localhost:7071/api/Predict with the following body:
 ```
{
  "SepalLength": 3.3,
  "SepalWidth": 1.6,
  "PetalLength": 0.2,
  "PetalWidth": 5.1
}
 ```

If all is well, the categorizer will return “Iris-verginica”.

## To deploy Skynet

… or whatever AI you are deploying from Visual Studio, go to your build settings in the toolbar.

 <img style="border:3px solid #021a40" src="/files/publish.png">

Select “Publish serverless_ai” to deploy your Azure Function app. 

 <img style="border:3px solid #021a40" src="/files/test_in_portal.png">

To test the app deployment in the Azure Portal, select you Azure Function app under **mlnetdemo** (or however you named it) and then pick the **Predict** function under that. Use the **Test** panel to the right of the screen to see your deployed app in action.

## Wrap-up 

This will place your iris categorizer out on Azure for other people to try.  Congratulations! You are now able to deploy artificial intelligences to the cloud.

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
