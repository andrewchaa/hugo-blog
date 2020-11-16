---
title: "Typed Configuration in ASP.NET Core"
date: 2020-11-15T19:45:09Z
draft: false
---
# Typed Configuration in ASP.NET Core

Another great thing I like is Typed Configuration in .NET Core. You create a class and bind the configuration section to it. It was possible before but it is much easier now.

```csharp
public class KeyVaultOptions
{
    public string TenantId { get; set; }
    public string ClientId { get; set; }
    public string ClientSecret { get; set; }
}

```

Then bind the DTO class to the config section.

```csharp
private static IServiceCollection AddConfigurations(this IServiceCollection services,
    IConfiguration configuration)
{
    services.Configure<KeyVaultOptions>(configuration.GetSection("KeyVault"));
    return services;
}

```

