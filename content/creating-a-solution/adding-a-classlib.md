---
title: "Adding a library"
date: 2019-12-26T15:25:12-05:00
draft: false
weight: 3
---

To add a non-deployable project to your solution, you can use the `classlib`
template from `dotnet new --list` command

`classlib` template creates an empty C# library project by default.

Here's an example:

```bash
dotnet new classlib --name MyClassLib --output src/MyClassLib

e.g.
dotnet new classlib --name NeverendingTeaShop.Application --output src/NeverendingTeaShop.Application
```

Once you've created a class library, you'll need to add it to the solution

```bash
dotnet sln [solution-file] add [csproj-file]

e.g.
dotnet sln NeverendingTeaShop.sln add src/NeverendingTeaShop.Application/NeverendingTeaShop.Application.csproj
```
