---
title: "Initial program structure"
date: 2019-10-06T13:06:31-04:00
draft: true
weight: 6
---

Here's a brief overview of the initial structure of each project that
was created. This section will illuminate how a C# program is structured
in different contexts (Web API, xUnit)

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
is `appsettings.<environment-name>.json`, where Development is a built-in environment in .NET Core. Development and Production
are built-in, but you can create your own by injecting `ASPNETCORE_Environment` variable into the runtime, via profiles
in `launchSettings.json`, or within your system environment (e.g. `export ASPNETCORE_Environment=Acceptance`)


## xUnit Project

Directory structure for an `xunit` project:

```shell script
[xUnit Project]
    - bin/ (git ignored directory)
    - obj/ (git ignored directory)
    - [xUnit Project].Tests.csproj
```
