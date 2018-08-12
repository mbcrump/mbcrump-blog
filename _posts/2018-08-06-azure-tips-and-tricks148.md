---
layout: post
title: "Azure Tips and Tricks Part 148 - Share Business Logic between Azure Functions"
excerpt: "Learn how to run share business logic between Azure Functions"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Share Business Logic between Azure Functions

A common scenario to share business logic between function is: I have an Azure Function that runs daily on a timer trigger and need the same function to run when I request it manually. While the template used may change you basically don't want to copy/paste the logic into another function. Instead, your function app architecture could look like:

```text
MyFunctionApp
|     host.json
|____ shared
|     |____ businessLogic.js
|____ function1
|     |____ index.js
|     |____ function.json
|____ function2
      |____ index.js
      |____ function.json
```


In the `shared` folder, you'd create a file named `businessLogic.js` and put your shared code.  

A sample in JS could be the following:

```javascript
module.exports = function (context, req) {
    // T
    context.res = {
        body: "<b>Hello World, from Azure Tips and Tricks</b>",
        status: 201,
        headers: {
            'content-type': "text/html"
        }
    };     
    context.done();
};
```
Then you'd create two separate functions called `function1` and `function2`. 

Then in your `function1/index.js` and `function2/index.js`, you would use the following lines of code that reference the shared logic folder and file. 

```javascript
var logic = require("../shared/businessLogic.js");
module.exports = logic;
```

Notice that each function has their own function.json. So here you could define them to be different triggers such as `function1` could be: 

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "type": "httpTrigger",
      "direction": "in",
      "name": "req",
      "methods": [
        "get",
        "post"
      ]
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ],
  "disabled": false
}
```

```json
and `function2` could be:

{
  "generatedBy": "Microsoft.NET.Sdk.Functions.Generator-1.0.0.0",
  "configurationSource": "attributes",
  "bindings": [
    {
      "type": "timerTrigger",
      "schedule": "0 0 */6 * * *",
      "useMonitor": true,
      "runOnStartup": false,
      "name": "myTimer"
    }
  ],
  "disabled": false,
  "scriptFile": "../bin/MichaelTest.dll",
  "entryPoint": "MichaelTest.SendTweet.Run"
}
```

As always, I hoped this help someone out there! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 