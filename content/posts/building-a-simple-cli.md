---
title: "Building a simple CLI"
date: 2020-11-15T19:45:09Z
draft: false
---
# Building a simple CLI

CLI, command-line interface, provides a very handy command interface that serves your face. If restful APIs are for machine, CLI is for human, especially developers.

First, Install package.

* commandlineparser: [https://github.com/commandlineparser/commandline](https://github.com/commandlineparser/commandline)

The below is a modified version of the quick example. I've added async and await as most of the time, I need async methods.

```csharp
using System;
using CommandLine;

namespace QuickStart
{
    class Program
    {
        public class Options
        {
            [Option('c', "cmd", Required = false, HelpText = "Your choice of command")]
            public string Command { get; set; }
        }

        static async Task Main(string[] args)
        {
            await Parser.Default.ParseArguments<Options>(args)
                .WithParsedAsync<Options>(async o =>
            {
                if (string.IsNullOrEmpty(o.Command))
                {
                    Console.WriteLine("Examples: \n");
                    Console.WriteLine("dotnet run --cmd add-domains");
                    Console.WriteLine("");
                }
            });
        }
    }
}
```

To help other users than me, it's good to show some examples. So if the command option is not give, I show some examples.

```bash
dotnet run

Examples:

dotnet run --cmd download
dotnet run --cmd detect-events
dotnet run --cmd document-event
dotnet run --cmd publish-to-wiki
dotnet run --cmd demo
```

It would be good to separate out execution code from the command parse logic. So I use command classes.

```csharp
static async Task Main(string[] args)
{
    await Parser.Default.ParseArguments<Options>(args)
        .WithParsedAsync<Options>(async o =>
    {
        if (string.IsNullOrEmpty(o.Command))
        {
            Console.WriteLine("Examples: \n");
            Console.WriteLine($"dotnet run --cmd {AddDomains}");
            Console.WriteLine("");
        } else if (o.Command == AddDomains)
        {
            new AddDomainsCommand().Run();
        }
    });
}

internal class AddDomainsCommand
{
    public void Run()
    {

    }
}
```

To do anything meaninful, we would need some service classes. So let's add them.

