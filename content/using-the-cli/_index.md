---
title: "⚙️ Using the .NET Core CLI"
date: 2019-09-26T13:11:52-04:00
draft: false
weight: 98
---

.NET Core CLI allows you to interact with the .NET Core runtime
as well as manage your .NET Core solutions and projects ([read more here](/getting-started/organizing-code))

The following is a brief overview of some of the more important and most likely daily commands that you want to
be familiar with.

### Viewing list of templates

Display a list of all solution and project templates that are available to generate a new solution or project.

```bash
dotnet new --list
```

### Retrieve all dependencies of each project in a solution

```bash
dotnet restore
```

[more on restoring dependencies](https://docs.microsoft.com/en-us/nuget/concepts/dependency-resolution)

### Creating a solution

```bash
# Basic invocation
dotnet sln new --name [name-of-solution] --output [path-to-new-solution]

# Example:
dotnet new sln --name NeverendingTeaShop --output NeverendingTeaShop/
```

### Creating a project

```bash
# Basic invocation
dotnet new [template] --name [name-of-project] --output [path-to-new-project]

# Example:
dotnet new webapi --name NeverendingTeaShop.API --output ./src/NeverendingTeaShop.API
dotnet new xunit --name NeverendingTeaShop.API.Tests --output ./tests/NeverendingTeaShop.API.Tests
```

### Run a deployable project

```bash
# Basic invocation
dotnet run [path-to-csproj]

# Example
dotnet run NeverendingTeaShop/src/NeverendingTeaShop.API
```

### Live reload changes when developing

```bash
# Watch a running application locally
dotnet watch run

# Watch tests
dotnet watch test
```

### Adding a NuGET package to a project

An example of adding `Serilog` nuget to a project

```bash
# If inside the project directory
dotnet add package Serilog

# If in root directory of a multi-project solution
dotnet add <path-to-project> package Serilog
```
