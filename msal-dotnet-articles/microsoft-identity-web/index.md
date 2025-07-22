---
title: Microsoft Identity Web
description: Learn how you can use Microsoft Identity Web to add authentication and authorization to web apps, web APIs, and daemon applications. 
author: Dickson-Mwendia
manager: CelesteDG
ms.author: jmprieur
ms.date: 07/21/2025
ms.service: msal
ms.subservice: microsoft-identity-web
ms.reviewer:
ms.topic: article
ms.custom: devx-track-csharp, aaddev
# Customer intent: As an application developer, I want to learn how Microsoft Identity Web can help me protect my services with the Microsoft identity platform. 
---

# Microsoft Identity Web authentication library

Microsoft Identity Web is a set of ASP.NET Core libraries that simplifies adding authentication and authorization support to web apps,  web APIs, and daemon apps integrating with the Microsoft identity platform. It provides a single-surface API convenience layer  that ties together ASP.NET or ASP.NET Core, their authentication middleware, and the [Microsoft Authentication Library (MSAL) for .NET](https://github.com/azuread/microsoft-authentication-library-for-dotnet) that acquires tokens. It can be installed via NuGet or by using a Visual Studio project template to create a new app project

## Supported application scenarios

When building ASP.NET Core web apps or web APIs that use Microsoft Entra ID or Microsoft Entra External ID for identity and access management (IAM), Microsoft Identity Web is recommended for these scenarios:

- [Service/daemon applications](/azure/active-directory/develop/scenario-daemon-overview)
- [Web app that signs in users](/azure/active-directory/develop/scenario-web-app-sign-user-overview)
- [Web app that signs in users and calls a web API on their behalf](/azure/active-directory/develop/scenario-web-app-call-api-overview)
- [Protected web API that only authenticated users can access](/azure/active-directory/develop/scenario-protected-web-api-overview)
- [Protected web API that calls another (downstream) web API on behalf of the signed-in user](/azure/active-directory/develop/scenario-web-api-call-api-overview)

## Modern authentication features

Microsoft Identity Web supports advanced authentication capabilities:

- **Managed Identity Support**: Simplified authentication for Azure-hosted applications without storing credentials
- **Workload Identity Federation**: Certificate-less authentication for Kubernetes and cloud-native applications
- **Continuous Access Evaluation (CAE)**: Enhanced security with real-time access control
- **Proof of Possession (PoP) Tokens**: Advanced token binding for high-security scenarios
- **OpenTelemetry Integration**: Built-in observability and monitoring capabilities

## Supported platforms

Microsoft identity web is available for .NET 8+, .NET 6+, .NET 4.8, and .NET Standard 2.0.

## Performance optimizations

Microsoft Identity Web leverages MSAL.NET's performance enhancements:

- **System.Text.Json**: Up to 60% faster JSON operations on .NET 6+ compared to Newtonsoft.Json
- **Optimized Token Caching**: Significant performance improvements for applications with large token caches
- **Memory Efficiency**: Reduced memory allocation and improved garbage collection performance
- **Legacy Cache Compatibility**: Optional legacy ADAL cache support that can be disabled for better performance

## Quick start

Get started with Microsoft Identity Web in minutes:

### ASP.NET Core Web App
```bash
# Create a new web app with authentication
dotnet new webapp --auth SingleOrg --client-id "your-client-id" --tenant-id "your-tenant-id"

# Add Microsoft Graph support
dotnet add package Microsoft.Identity.Web.MicrosoftGraph
```

### ASP.NET Core Web API
```bash
# Create a new web API with authentication
dotnet new webapi --auth SingleOrg --client-id "your-client-id" --tenant-id "your-tenant-id"

# Add downstream API support
dotnet add package Microsoft.Identity.Web.DownstreamApi
```

### Key configuration in `appsettings.json`:
```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "TenantId": "your-tenant-id",
    "ClientId": "your-client-id",
    "ClientSecret": "your-client-secret",
    "CallbackPath": "/signin-oidc"
  }
}
```

## Install from NuGet

Microsoft Identity Web is available on NuGet as a set of packages that provide modular functionality based on application requirements. Use the .NET CLI's `dotnet add` command or Visual Studio's **NuGet Package Manager** to install the appropriate packages:

- [Microsoft.Identity.Web](https://www.nuget.org/packages/Microsoft.Identity.Web) - The main package for ASP.NET Core applications.
- [Microsoft.Identity.Web.OWIN](https://www.nuget.org/packages/Microsoft.Identity.Web.OWIN) - The main package for ASP.NET (OWIN) applications.
- [Microsoft.Identity.Web.TokenAcquisition](https://www.nuget.org/packages/Microsoft.Identity.Web.TokenAcquisition) - The main package for other types of applications (daemon apps on .NET Framework or .NET). Microsoft.Identity.Web and Microsoft.Identity.Web.OWIN reference this package. 
- [Microsoft.Identity.Web.UI](https://www.nuget.org/packages/Microsoft.Identity.Web.UI) - Optional, for ASP.NET Core web apps. Adds UI for user sign-in and sign-out and an associated controller for web apps.
- [Microsoft.Identity.Web.MicrosoftGraph](https://www.nuget.org/packages/Microsoft.Identity.Web.MicrosoftGraph) - Optional. Provides simplified interaction with the Microsoft Graph API.
- [Microsoft.Identity.Web.MicrosoftGraphBeta](https://www.nuget.org/packages/Microsoft.Identity.Web.MicrosoftGraphBeta) - Optional. Provides simplified interaction with the Microsoft Graph API [beta endpoint](/graph/api/overview?view=graph-rest-beta&preserve-view=true).
- [Microsoft.Identity.Web.DownstreamApi](https://www.nuget.org/packages/Microsoft.Identity.Web.DownstreamApi) - Optional. Provides simplified and declarative interaction with downstream APIs.
- [Microsoft.Identity.Web.Azure](https://www.nuget.org/packages/Microsoft.Identity.Web.Azure) - Optional. Provides simplified interaction with the Azure SDKs.

The following NuGet packages, which are referenced by the packages above, can also be used directly with MSAL.NET:

- [Microsoft.Identity.Web.TokenCache](https://www.nuget.org/packages/Microsoft.Identity.Web.TokenCache) - Provides simplified token cache serializers for MSAL.NET (In memory, distributed cache)
- [Microsoft.Identity.Web.Certificate](https://www.nuget.org/packages/Microsoft.Identity.Web.Certificate) - Provides simplified interaction with certificates
- [Microsoft.Identity.Web.Certificateless](https://www.nuget.org/packages/Microsoft.Identity.Web.Certificateless) - Provides simplified interaction with other forms of credentials not based on certificates (signed assertions from [workload identity federation](/azure/active-directory/workload-identities/workload-identity-federation), integration with Azure Kubernetes Services (AKS), ...)

## Install by using a Visual Studio project template

Several project templates that use *Microsoft.Identity.Web* are included in .NET SDK versions 6.0 and above.

### .NET 6.0+ - Project templates included

The Microsoft Identity Web project templates are included in .NET SDK versions 6.0 and above.

In the following example, .NET CLI command creates a Blazor Server project that includes Microsoft Identity Web.

```dotnetcli
dotnet new webapp --auth SingleOrg --calls-graph --client-id "00001111-aaaa-2222-bbbb-3333cccc4444" --tenant-id "aaaabbbb-0000-cccc-1111-dddd2222eeee" --output my-blazor-app
```
<!-- 
## Conceptual documentation

-->


### Getting started with Microsoft Identity Web

1. Learn about [Scenarios](./getting-started/scenarios.md).
1. You'll need to [register your app](/azure/active-directory/develop/quickstart-register-app) with Microsoft Entra ID.

## Cloud-native and modern deployment scenarios

Microsoft Identity Web supports modern deployment patterns:

- **Azure App Service**: Integrated authentication with minimal configuration
- **Azure Container Instances**: Managed identity support for containerized applications  
- **Azure Kubernetes Service (AKS)**: Workload identity federation for pod-level authentication
- **Azure Functions**: Optimized performance for serverless scenarios
- **Docker Containers**: Simplified authentication for containerized web applications

For production deployments, consider:
- Using managed identities to eliminate credential storage
- Implementing Continuous Access Evaluation for enhanced security
- Enabling OpenTelemetry for comprehensive monitoring

## Security best practices

Follow these security recommendations when using Microsoft Identity Web:

### Credential Management
- **Use Managed Identities**: Eliminate stored secrets for Azure-hosted applications
- **Azure Key Vault**: Store certificates and secrets securely outside your application
- **Environment Variables**: Never commit secrets to source control
- **Workload Identity Federation**: Use certificate-less authentication for Kubernetes workloads

### Token Security
- **Token Caching**: Use appropriate cache serialization based on your deployment scenario
- **Scope Management**: Request only the minimum required permissions (principle of least privilege)
- **Token Lifetime**: Configure appropriate token lifetimes based on security requirements
- **Continuous Access Evaluation**: Enable CAE for real-time access control and token revocation

### Network Security
- **HTTPS Only**: Always use HTTPS in production environments
- **Certificate Validation**: Implement proper certificate validation for API calls
- **CORS Configuration**: Configure CORS appropriately for single-page applications
- **Content Security Policy**: Implement CSP headers to prevent XSS attacks

### Monitoring and Compliance
- **Audit Logging**: Enable comprehensive audit logging for authentication events
- **Sign-in Analytics**: Monitor sign-in patterns and anomalies
- **Conditional Access**: Implement conditional access policies based on risk assessment
- **Compliance**: Ensure your implementation meets regulatory requirements (SOC2, FedRAMP, etc.)

## Troubleshooting common issues

### Authentication Failures
- **Redirect URI Mismatch**: Ensure your redirect URI in Azure AD matches your application configuration
- **Tenant Configuration**: Verify tenant ID and client ID are correctly configured
- **Permissions**: Check that required API permissions are granted and admin consent is provided
- **Certificate Issues**: Validate certificate thumbprints and expiration dates

### Performance Issues
- **Token Cache Size**: Monitor token cache size and implement appropriate cleanup strategies
- **Concurrent Requests**: Implement proper handling for concurrent token acquisition requests
- **Memory Usage**: Profile memory usage, especially with large user bases
- **Network Latency**: Consider token cache preloading for high-traffic scenarios

### Development Environment Issues
- **Local Development**: Use development certificates and configure local redirect URIs
- **HTTPS Requirements**: Ensure HTTPS is configured for local development
- **Port Configuration**: Verify callback URLs match your development port configuration
- **Browser Cache**: Clear browser cache when testing authentication flows

### Production Deployment Issues
- **Health Checks**: Implement health checks that verify authentication service availability
- **Load Balancing**: Configure session affinity appropriately for load-balanced deployments
- **Container Deployments**: Ensure proper configuration for containerized applications
- **Key Rotation**: Implement procedures for certificate and secret rotation

### Diagnostic Tools
- **Logging**: Enable detailed logging to troubleshoot authentication issues
- **Fiddler/Network Traces**: Capture network traffic to analyze OAuth flows
- **Azure AD Sign-in Logs**: Review Azure AD sign-in logs for detailed error information
- **Application Insights**: Use Application Insights for comprehensive application monitoring

## Migration guidance

### From ADAL.NET
Microsoft Identity Web provides a modern replacement for ADAL.NET with significant improvements:

- **Enhanced Security**: Built-in support for modern authentication protocols
- **Better Performance**: Optimized token caching and reduced memory footprint  
- **Simplified APIs**: Reduced boilerplate code and easier configuration
- **Active Support**: ADAL reached end-of-life in June 2023

**Key migration steps:**
1. Update NuGet packages from ADAL to Microsoft.Identity.Web
2. Replace ADAL configuration with Microsoft Identity Web configuration
3. Update authentication middleware registration
4. Migrate token acquisition calls to use Microsoft Identity Web APIs
5. Test all authentication flows thoroughly

### From ASP.NET Core 2.x Authentication
Upgrading from built-in ASP.NET Core authentication:

- **Enhanced Token Management**: Automatic token refresh and caching
- **Microsoft Graph Integration**: Built-in support for Microsoft Graph APIs
- **Advanced Features**: Support for CAE, PoP tokens, and managed identities
- **Simplified Configuration**: Reduced configuration complexity

### From Custom OAuth Implementations
Benefits of migrating to Microsoft Identity Web:

- **Reduced Maintenance**: No need to implement OAuth flows manually
- **Security Updates**: Automatic security updates and vulnerability patches
- **Microsoft Graph Integration**: Seamless integration with Microsoft 365 services
- **Enterprise Features**: Built-in support for enterprise scenarios like multi-tenant applications

## Advanced configuration

### Multi-tenant Applications
Configure your application to support users from multiple Azure AD tenants:

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "TenantId": "common", // or "organizations" for work/school accounts only
    "ClientId": "your-client-id"
  }
}
```

### Custom Claims and Transformations
Transform claims or add custom claims to the user identity:

```csharp
services.AddMicrosoftIdentityWebAppAuthentication(Configuration)
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddInMemoryTokenCaches();

services.Configure<OpenIdConnectOptions>(options =>
{
    options.Events.OnTokenValidated = async context =>
    {
        // Add custom claims transformation logic
        var identity = (ClaimsIdentity)context.Principal.Identity;
        identity.AddClaim(new Claim("custom-claim", "custom-value"));
        await Task.CompletedTask;
    };
});
```

### Conditional Access and CAE
Enable Continuous Access Evaluation for enhanced security:

```csharp
services.AddMicrosoftIdentityWebAppAuthentication(Configuration)
    .EnableTokenAcquisitionToCallDownstreamApi(new string[] { "https://graph.microsoft.com/User.Read" })
    .AddMicrosoftGraph(Configuration.GetSection("MicrosoftGraph"))
    .AddInMemoryTokenCaches();

// Configure CAE
services.Configure<MsalDistributedTokenCacheAdapterOptions>(options =>
{
    options.DisableLegacyAdalCache = true; // Improve performance
});
```

### Custom Token Caching
Implement distributed token caching for production scenarios:

```csharp
services.AddMicrosoftIdentityWebAppAuthentication(Configuration)
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddDistributedTokenCaches();

// Add Redis or SQL Server distributed cache
services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = "your-redis-connection-string";
});
```

### Logging and Monitoring
Configure comprehensive logging and monitoring:

```csharp
services.AddLogging(builder =>
{
    builder.AddApplicationInsights();
    builder.AddConsole();
});

// Enable MSAL logging
services.Configure<MsalDistributedTokenCacheAdapterOptions>(options =>
{
    options.EnablePiiLogging = false; // Set to true only in development
});
```

## Samples

See [our comprehensive sample list](/azure/active-directory/develop/active-directory-v2-code-samples).

## Related documentation

### Core Documentation
- [Microsoft Identity Web GitHub Repository](https://github.com/AzureAD/microsoft-identity-web)
- [Microsoft Authentication Library (MSAL) for .NET](../index.md)
- [Microsoft identity platform documentation](/entra/identity-platform/)
- [Azure Active Directory documentation](/entra/fundamentals/)

### Advanced Topics
- [Token cache serialization](../how-to/token-cache-serialization.md)
- [High availability guidance](../advanced/high-availability.md)
- [Performance testing and optimization](../advanced/performance-testing.md)
- [Monitoring and telemetry](../advanced/monitoring.md)
- [Managed identity support](../advanced/managed-identity.md)
- [Proof of possession tokens](../advanced/proof-of-possession-tokens.md)

### API References
- [Microsoft.Identity.Web API Reference](https://docs.microsoft.com/dotnet/api/microsoft.identity.web)
- [Microsoft.Identity.Client API Reference](https://docs.microsoft.com/dotnet/api/microsoft.identity.client)
- [Microsoft Graph .NET SDK](https://docs.microsoft.com/graph/sdks/sdk-installation#install-the-microsoft-graph-net-sdk)

### Support and Community
- [Stack Overflow - microsoft-identity-web](https://stackoverflow.com/questions/tagged/microsoft-identity-web)
- [Microsoft Q&A - Microsoft Identity Platform](https://docs.microsoft.com/answers/topics/azure-ad-dev-support.html)
- [GitHub Issues](https://github.com/AzureAD/microsoft-identity-web/issues)
- [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/bd-p/Azure-Active-Directory-Identity)

## Next steps

1. **Choose your scenario**: Review the [supported application scenarios](#supported-application-scenarios) to identify your use case
2. **Set up your environment**: Follow the [quick start guide](#quick-start) to create your first application
3. **Register your application**: [Register your app in Azure AD](/azure/active-directory/develop/quickstart-register-app)
4. **Implement authentication**: Add Microsoft Identity Web to your application using the appropriate NuGet packages
5. **Test and deploy**: Implement [security best practices](#security-best-practices) and deploy to production
6. **Monitor and maintain**: Set up [monitoring and logging](#advanced-configuration) for your production application

For detailed step-by-step guidance, see our [comprehensive tutorials and samples](/entra/identity-platform/sample-v2-code).
