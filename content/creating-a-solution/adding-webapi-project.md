---
title: "Adding a Web API project"
date: 2019-09-27T16:33:06-04:00
draft: false
weight: 2
tags: ["project", "webapi", "api", "xunit"]
---

{{%expand "TL;DR"%}}
```bash
# Create a .NET Core Web API Project
dotnet new webapi --name [name-of-project] --output [path-to-new-project-on-file-system]
# Add project to the root Solution
dotnet sln [path-to-solution-file] add [path-to-api-project-csproj]
```
{{%/expand%}}

Once you've created a [solution](/creating-a-solution/starting-from-scratch),
you can add projects to it, following the organizational structure described in
[Organizing Code](/getting-started/organizing-code) section.

A project is defined by a `*.csproj` file, which is the project descriptor file.

## Creating a Web API project

In this section, we will create a .NET Core Web API project and a complimentary
.NET Core test project with xUnit test framework.

{{<mermaid>}}
graph RL;
    id2("<b>NeverendingTeaShop.API.Tests</b><br/>(.NET Core xUnit)")-->id1("<b>NeverendingTeaShop.API</b><br/>(.NET Core Web API)");
{{</mermaid>}}

The Web API source project is the project where our API related code will live
(i.e. controllers, etc.).

The xUnit test project is the project where our test code for the API project will live.

{{% notice note %}}
xUnit is a popular test framework from Microsoft and maintained as an open source project by the .NET Foundation. [More here](https://xunit.net/)
{{% /notice %}}

### Source project

```bash
# Create a .NET Core Web API Project
dotnet new webapi --name [name-of-project] --output [path-to-new-project-on-file-system]
# Add project to the root Solution
dotnet sln [path-to-solution-file] add [path-to-api-project-csproj]

# e.g.
dotnet new webapi --name NeverendingTeaShop.API --output src/NeverendingTeaShop.API
dotnet sln NeverendingTeaShop.sln add src/NeverendingTeaShop.API/NeverendingTeaShop.API.csproj
```

These commands will create a Web API .NET Core project in `src/NeverendingTeaShop.API`
directory and bind them to the root Solution. Binding a project (aka adding a
  reference) will ensure the root Solution can coordinate
each project's lifecycle, from running, building, and publishing.

{{% notice note %}}
The `webapi` part is just a template for a specific project purpose.
In this case, .NET Core CLI creates a base
.NET Core project with a web server ready to service API requests.
[View a list of available templates with this command](/using-the-cli/#viewing-list-of-templates)
{{% /notice %}}

### Test project

Source and test projects are separated into their own respective directories in
the .NET world, so no test code will be packaged into an artifact at the publish (aka package)
stage of the development lifecycle.

```bash
# Create a .NET Core xUnit Project
dotnet new xunit --name [name-of-project] --output [path-to-new-test-project-on-file-system]
# Add project to the root Solution
dotnet sln [path-to-solution-file] add [path-to-test-project-csproj]
# Add reference of the original source project
dotnet add [path-to-test-project-csproj] reference [path-to-source-project-csproj]

# e.g.
dotnet new xunit --name NeverendingTeaShop.API.Tests --output src/NeverendingTeaShop.API.Tests
dotnet sln NeverendingTeaShop.sln add src/NeverendingTeaShop.API.Tests/NeverendingTeaShop.API.Tests.csproj
dotnet add tests/NeverendingTeaShop.API.Tests/NeverendingTeaShop.API.Tests.csproj reference src/NeverendingTeaShop.API/NeverendingTeaShop.API.csproj

```

These commands will create a new .NET Core xUnit project and bind them to the root Solution.

---

#### Footnotes

- [dotnet new command reference](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new)
