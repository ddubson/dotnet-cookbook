---
title: "Adding Projects"
date: 2019-09-27T16:33:06-04:00
draft: false
weight: 2
---

Once you've created a [Solution](/creating-a-solution/starting-from-scratch), you can add projects to it, 
following the organizational structure described in [Organizing Code](/getting-started/organizing-code) section.

{{% notice tip %}}
Source and test projects are separated into their own respective directories
{{% /notice %}}

A project is defined by a `*.csproj` file, which is the project descriptor file.

## Creating a Web API

In this section, we will create a .NET Core Web API project and a .NET Core xUnit project. 

e.g.
```mermaid
graph RL;
    id2("<b>GoodProduct.API.Tests</b><br/>(.NET Core xUnit)")-->id1("<b>GoodProduct.API</b><br/>(.NET Core Web API)");
```
The Web API source project is the project where our API related code will live (i.e. controllers, etc.). 

The xUnit project is the project where our test code for the API project will live.

{{% notice note %}}
xUnit is a popular test framework from Microsoft and maintained as an open source project by the .NET Foundation. 
[More here](https://xunit.net/)
{{% /notice %}}

### Source project

```bash
# Create a .NET Core Web API Project
dotnet new webapi --name [name-of-project] --output [path-to-new-project-on-file-system]
# Add project to the root Solution
dotnet sln [path-to-solution-file] add [path-to-api-project-csproj]

# e.g.
dotnet new webapi --name GoodProduct.API --output src/GoodProduct.API
dotnet sln GoodProduct.sln add src/GoodProduct.API/GoodProduct.API.csproj
```

These commands will create a Web API .NET Core project in `src/GoodProduct.API` directory and bind them
to the root Solution. Binding a project (aka adding a reference) will ensure the root Solution can coordinate
each project's lifecycle, from running, building, and publishing.

{{% notice note %}}
The `Web API` part is just a template for a specific project purpose. In this case, .NET Core CLI creates a base
.NET Core project with a web server ready to service API requests. 
[View a list of available templates with this command](/using-the-cli/#viewing-list-of-templates)
{{% /notice %}}

### Test project

```bash
# Create a .NET Core xUnit Project
dotnet new xunit --name [name-of-project] --output [path-to-new-test-project-on-file-system]
# Add project to the root Solution
dotnet sln [path-to-solution-file] add [path-to-test-project-csproj]
# Add reference of the original source project
dotnet add [path-to-test-project-csproj] reference [path-to-source-project-csproj]

# e.g.
dotnet new xunit --name GoodProduct.API.Tests --output src/GoodProduct.API.Tests
dotnet sln GoodProduct.sln add src/GoodProduct.API.Tests/GoodProduct.API.Tests.csproj
dotnet add tests/GoodProduct.API.Tests/GoodProduct.API.Tests.csproj reference src/GoodProduct.API/GoodProduct.API.csproj

```

These commands will create a new .NET Core xUnit project and bind them to the root Solution.

---

#### Footnotes

- [dotnet new command reference](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new)
