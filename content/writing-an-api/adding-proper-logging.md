---
title: "Application logging with Serilog"
date: 2020-07-02T17:13:55-04:00
draft: false
weight: 4
tags: ['logging', 'serilog', '12-factor']
---

Logging is an important aspect of an application -- 
it is the **11th** factor of the [12-factor app](https://12factor.net/logs)

Deploying an application to the cloud almost surely requires a proper logging mechanism to track 
potential errors, when they happened, how often they might be happening, and at what specific times 
they are occurring. Aside from the normal hum of the application, if deploying an application that may 
span multiple instances as is standard procedure for many cloud applications, it is important to use a robust
logging mechanism that can flush application logs to logging systems, such as LogStash or Splunk.

.NET Core provides a unified API for logging and has built-in and third-party **providers** (i.e. 
implementations) of those logging interfaces.

For this example we'll use a popular 3rd-party implementation of .NET Core's logging API 
called **Serilog**

## Adding Serilog to your application

To add Serilog to your .NET Core project, you can use the trusty .NET CLI:

```bash
# If inside the project directory
dotnet add package Serilog
dotnet add package Serilog.Sinks.Console
dotnet add package Serilog.AspNetCore

# OR if in root directory of a multi-project solution
dotnet add <path-to-project> package Serilog
dotnet add <path-to-project> package Serilog.Sinks.Console
dotnet add <path-to-project> package Serilog.AspNetCore
```

Next, add relevant Serilog configuration code to the start of your program, usually located 
in `Program.cs` of a .NET Core Web API application. The description for each section is in the 
code below. 

```c#
using System.IO;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Hosting;
using Serilog;

namespace myapp {
    public class Program
    {
        // Configuration settings for the application, first loaded 
        // from appsettings.json, overridden by environment variables. 
        // This file should contain, at the very least, default log levels for Serilog
        private static IConfiguration Configuration { get; } = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
                .AddEnvironmentVariables()
                .Build();

        public static void Main(string[] args)
        {
            // Primary configuration for Serilog for the application
            Log.Logger = new LoggerConfiguration()
                .WriteTo.Console(theme: AnsiColorTheme.Code)  // Tell Serilog to write to Console
                .ReadFrom.Configuration(Configuration)        // Loaded Serilog settings
                .CreateLogger();

            Host.CreateDefaultBuilder(args)
                .UseSerilog()  // Tell the web host Serilog is used.
                .Build()
                .Run();
        }
    }
}
```

For other types of applications, 
refer to [Serilog's Getting Started guide](https://github.com/serilog/serilog/wiki/Getting-Started)

Next, make sure `appsettings.json` configuration file contains the following section:

```json
{ 
  "Serilog": {
    "MinimumLevel": {
      "Default": "Debug",         
      "Override": {
        "System": "Information",
        "Microsoft": "Information"
      }
    }
  }
}
```

[Here's a full description of Serilog configuration that might come in handy](https://github.com/serilog/serilog/wiki/Configuration-Basics)

## Using a logger in your application

To use Serilog in a class method or function, there are a couple of ways of invoking it.

You can use a static import and invocation for times when you are unable to inject the logger via 
constructor or method signature.

```c#
using Serilog;

Log.Information("Hello, World!");
Log.Error("This class method was not able to perform an operation because of very good reasons");
Log.Critical("The application has suffered a serious issue");
```

You can also use the standard .NET Core API `ILogger<T>` injection via constructor

```c#
using Microsoft.Extensions.Logging;

namespace myapp 
{
    public class MyClass 
    {
        private readonly ILogger<MyClass> _logger;

        public MyClass(ILogger<MyClass> logger) 
        {
            _logger = logger;
        }

        public void MyMethod() 
        {
            _logger.LogInformation("Hi!");
        }
    }
}
```

## Sinks - or "where your log messages are written to"

Log sinks are designated targets of where you would like the logger mechanism to write messages to.

The no-frills, get-you-started sink to use is the **Console** sink.

Some examples of sinks in Serilog are:

- **Console** - messages are displayed to you on the command line and disappear after the session ends.
- **File** - messages are written to files on the local or attached file system.
- **Splunk** - messages are directly sent to Splunk

[Serilog has a vast array of Sinks, here's the full list](https://github.com/serilog/serilog/wiki/Provided-Sinks)

---

## References

- https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-3.1
- https://github.com/serilog/serilog/wiki/Getting-Started