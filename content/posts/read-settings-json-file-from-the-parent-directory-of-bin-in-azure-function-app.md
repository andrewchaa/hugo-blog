---
title: "Read settings json file from the parent directory of bin in Azure Function app"
date: 2020-11-15T19:45:09Z
draft: false
---
# Read settings json file from the parent directory of "bin" in Azure Function app

I recently I deployed a function app. I used appsettings.json as usual but encountered an issue. First, unlike ASP.NET Core, appsettings.json wasn't published by default. Second, when it was published, it wasn't published in the "bin" directory where all assemblies are published. It was in the parent directory of the "bin". So IServiceCollection couldn't read the settings json file.

## Publish appsettings.json

Update the project file to publish the settings json file

```markup
<ItemGroup>
  <Content Include="host.json">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
  </Content>
  <Content Include="appsettings.json">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
  </Content>
</ItemGroup>
```

## Relative path and absolute path

```csharp
var settingPath = Path.GetFullPath(Path.Combine(@"../appsettings.json"));

var configBuilder = new ConfigurationBuilder();
configBuilder.AddJsonFile("appsettings.json", optional: true, reloadOnChange: true);
configBuilder.AddJsonFile(settingPath, optional: true, reloadOnChange: true);

var config = configBuilder.Build();
Services.Configure<ChatRoomOptions>(config.GetSection("chatRoom"));
```

