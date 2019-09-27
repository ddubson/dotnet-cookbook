---
title: "Using the .NET Core CLI"
date: 2019-09-26T13:11:52-04:00
draft: false
weight: 99
---

.NET Core CLI allows you to interact with the .NET Core runtime
as well as manage your .NET Core solutions and projects ([read more here](./organizing-code.md))

The following is a brief overview of some of the more important and most likely daily commands that you want to
be familiar with.

### Creating a solution 

```bash
# Basic invocation
dotnet sln new --name [name-of-solution] --output [path-to-new-solution]

# Example:
dotnet new sln --name GoodProduct --output GoodProduct/
```

### Creating a project

```bash
# Basic invocation
dotnet new [template] --name [name-of-project] --output [path-to-new-project]

# Example:
dotnet new webapi --name GoodProduct.API --output ./src/GoodProduct.API
dotnet new xunit --name GoodProduct.API.Tests --output ./tests/GoodProduct.API.Tests
```

### Run a deployable project

```bash
# Basic invocation
dotnet run [path-to-csproj]

# Example
dotnet run GoodProduct/src/GoodProduct.API
```
