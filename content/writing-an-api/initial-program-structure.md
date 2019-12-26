---
title: "Initial program structure"
date: 2019-10-06T13:06:31-04:00
draft: false
weight: 3
tags: ['program structure', 'organizing code', 'project structure', 'api', 'webapi']
---

Here's a brief overview of the initial structure of each project that
was created. This section will illuminate how a C# program is structured
in the context of a Web API

## Web API Project

A Web API project is a C# program that is pre-packaged with a few frameworks
that enable Web features.

Directory structure for a `webapi` project:

```shell script
[Project]
    - bin/ (git ignored directory)
    - obj/ (git ignored directory)
    - Properties/
      - launchSettings.json
    - appsettings.Development.json
    - appsettings.json
    - [Project].csproj
    - Program.cs
    - Startup.cs
```

1. `bin/` and `obj/` directories are compiled object and binary directories. These should be ignored by Git
2. `Properties/launchSettings.json` is a launch descriptor file for each debug profile. When you run `dotnet run --project [project-path]`,
you can specify a specific profile to run in, and each profile can have its own environment variables. By default,
the run command executes the profile with the name of the project, but you can specify your own.
3. `appsettings.json` and `appsettings.Development.json` are project environment settings used to store environment
variables for the application. Analogous in Spring Boot/Java are `application.yml` files. The convention for each file
is `appsettings.<environment-name>.json`, where <environment-name> is a built-in environment in .NET Core. Development
and Production are built-in, but you can create your own by injecting `ASPNETCORE_Environment` variable into the
runtime, via profiles in `launchSettings.json`, or within your system environment
(e.g. `export ASPNETCORE_Environment=Acceptance`)
4. `appsettings.json` is a universal application settings file. All environment variables defined here will apply to
all environments. Add environment variables that are universal across all environments.
5. `Program.cs` is the main entry point of the application which contains the `main` function. Every C# deployable
project as a `main` method.
6. `Startup.cs` is the main service and configuration definition file. This is where the Dependency Injection container
is managed. The class within the file is read by the internal web host managed by .NET Core.

---

## xUnit Project

Directory structure for an `xunit` project:

```shell script
[xUnit Project]
    - bin/ (git ignored directory)
    - obj/ (git ignored directory)
    - [xUnit Project].Tests.csproj
```

xUnit projects are empty .NET Core projects that come packaged with xUnit framework and test runner.
