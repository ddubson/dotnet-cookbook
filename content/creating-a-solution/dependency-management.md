---
title: "Dependency management"
date: 2019-09-30T12:40:17-04:00
draft: false
weight: 3
---

Each project will need its own dependencies from external libraries or 
references to another project in the same solution.

The packages that a project references are described in the project's `csproj` file.

### External libraries with NuGet

NuGet is a package manager for .NET

NuGet Gallery is the central package repository for .NET libraries
You can find its [directory here](https://www.nuget.org/)

#### Adding a dependency to a project

Let's add a dependency to a project by using an example package `Newtonsoft.Json` which is a popular 
Json framework for .NET that is published in the central repository

```bash
dotnet add package Newtonsoft.Json
```

The previous command should be run within the project folder that you 
want to add the dependency to.

An example of external packages that a project uses within the project's `csproj` file

```xml
<ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.9.0" />
    <PackageReference Include="xunit" Version="2.4.0" />
    <PackageReference Include="xunit.runner.visualstudio" Version="2.4.0" />
    <PackageReference Include="Newtonsoft.Json" Version="12.0.3-beta1" />
</ItemGroup>
```

#### Fetching dependencies

When you clone a fresh copy of the codebase, or if you pull in new changes from Git that involve
added dependencies, you will want to **restore** (aka fetch) dependencies on your local development machine.

```bash
dotnet restore
```

### Adding project dependencies within a Solution

If you want to add a reference of one project to another, in the case of
needing to use the resources of another project, you can do so:

```bash
dotnet add [path-to-project] references [path-to-project-to-be-referenced]

# e.g. add source project reference to a test project
dotnet add tests/NeverendingTeaShop.API.Tests/NeverendingTeaShop.API.Tests.csproj reference src/NeverendingTeaShop.API/NeverendingTeaShop.API.csproj 
```

An example of a project reference that was created:

```xml
<ItemGroup>
    <ProjectReference Include="..\..\src\NeverendingTeaShop.API\NeverendingTeaShop.API.csproj" />
</ItemGroup>
```
