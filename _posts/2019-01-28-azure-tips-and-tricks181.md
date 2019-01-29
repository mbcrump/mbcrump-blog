---
layout: post
title: "Azure Tips and Tricks Part 181 - Taking a peek at Azure Key Vault Part 2 of 2"
excerpt: "Learn how to use taking a peek at azure key vault part 2 of 2"
tags: [azure, app service, portal, resources]
share: true
comments: true
---
 
**Help wanted!:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}


## Taking a peek at Azure Key Vault Part 2 of 2

In the [previous post](https://www.michaelcrump.net/azure-tips-and-tricks180), you set up Key Vault and added a secret via the Azure portal. Now you'll see how to securely access that secret programmatically. Let's start by creating a ASP.NET Core API app in Visual Studio (or you can [grab the completed project here](https://github.com/mbcrump/azure-key-vault)): 

<img style="border:3px solid #021a40" src="/files/new-api-app.png">

After the project is generated, add a new controller file called **SecretController.cs** with the following code.

```csharp
using Microsoft.AspNetCore.Mvc;

namespace KeyVaultApi.Controllers
{
    [Route("secret")]
    [ApiController]
    public class SecretController : ControllerBase
    {
        // GET api/values
        [HttpGet]
        public IActionResult Get()
        {
            string secret = "TBD";
            return Ok(new { Secret = secret });
        }
    }
}
```
As you might expect, the response from a browser request (or a tool like [Postman](https://www.getpostman.com/)) looks like:

<img style="border:3px solid #021a40" src="/files/browser-1.png">

To retrieve the secret from Key Vault, you'll want to pull in the [**Microsoft.Azure.KeyVault**](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) and [**Microsoft.Azure.Services.AppAuthentication**](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) NuGet packages. The **KeyVaultClient** class is the entry point for interacting with the vault, and the client code is actually pretty simple. Here the Key Vault service name is *fort-knox* and the secret's name is *deep-thought*; you should provide the appropriate values for your service.

```csharp
public async Task<IActionResult> Get()
{
	string secret = "TBD";

	var kvClient = new KeyVaultClient(authCallback);   
	secret = (await kvClient.GetSecretAsync(
		"https://fort-knox.vault.azure.net","deep-thought")).Value;

	return Ok(new { Secret = secret });
}
```

It's the authentication process (the missing implementation of **authCallback** in the code above) that has historically been a bit tricky; however, with [Azure AD Managed Service Identity (MSI)](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview) it's very straightforward. 

Initialize, **authCallback** (right after the initialization of the **secret** variable) as follows:

```csharp
	var authCallback = new KeyVaultClient.AuthenticationCallback
			(new AzureServiceTokenProvider().KeyVaultTokenCallback);
```

This creates a callback method that uses the **AzureServiceTokenProvider** class to access Key Vault on behalf of the application, without explicit use of secrets or certificates. 

During development, if you are signed in via the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest), the app will authenticate using that identity. Of course, that identity needs requisite (Get) access to secrets in Key Vault, but if it's the same user that set up the secret, it already has more permissions than needed.

To set up the application to run within Azure, create a new API app in the Azure portal, and via the **Managed service identity** option under **Settings**, select **On** to register with Azure Active Directory. This creates a service principal that the API app can use to authenticate itself to other Azure services like Key Vault. 

<img style="border:3px solid #021a40" src="/files/msi.png">

At this point, your Azure Key Vault does not have an access policy associated with this new identity, so any attempts to run the app in Azure would result in a Forbidden (403) error. To remedy, create a new policy that refers to the API app you just created (or more precisely to the MSI associated with that API app). For purposes of this exercise, the only needed operation is to get secrets from Key Vault.

<img style="border:3px solid #021a40" src="/files/access-policy.png">

Now, you can deploy the application and run it from Azure as well.

<img style="border:3px solid #021a40" src="/files/browser-2.png">

If you are building ASP.NET Core applications, you should also be aware of the Azure Key Vault configuration provider, which extends the [ASP.NET Core configuration provider](https://docs.microsoft.com/en-us/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1) to coalesce configuration data from multiple sources and expose it via dependency injection to your controllers.

In the **Program.cs** of your ASP.NET Core application, add the following call to **ConfigureAppConfiguration** to first get the name of the Key Vault from standard app properties and then use the **AddAzureKeyVault** extension method to gather all the names of the Key Vault secrets into the **IConfiguration** reference. Note, because the extension *enumerates* the secrets in Key Vault, you will need to grant the MSI List as well as Get permissions on the Key Vault instance.

```csharp
    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((context, config) =>
            {
                var builtConfig = config.Build();

                var authCallback = new KeyVaultClient.AuthenticationCallback
                    (new AzureServiceTokenProvider().KeyVaultTokenCallback);
                var kvClient = new KeyVaultClient(authCallback);

                config.AddAzureKeyVault(
                    $"https://{builtConfig["Vault"]}.vault.azure.net/",
                    kvClient,
                    new DefaultKeyVaultSecretManager()
                );
            })
            .UseStartup<Startup>();
```
The complete body of the controller then becomes

```csharp
    [Route("secret")]
    [ApiController]
    public class SecretController : ControllerBase
    {
        private readonly IConfiguration _config;
        public SecretController(IConfiguration config)
        {
            _config = config;
        }

        [HttpGet]
        public IActionResult Get()
        {
            return Ok(new { Secret = _config.GetValue<string>("deep-thought") });
        }
    }
```

For more on this subject, [Use Key Vault from App Service with Managed Service Identity](https://github.com/Azure-Samples/app-service-msi-keyvault-dotnet) on GitHub has a larger sample of using MSI to authenticate to Key Vault. Additionally, you can find [examples](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-use-from-web-application) that cover manual application registration using client secrets and certificates; however, those techniques are no longer recommended whenever MSI can be used.

I hope this helps someone out there!

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
