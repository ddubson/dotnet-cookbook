---
title: "Organizing Code"
date: 2019-09-26T09:02:31-04:00
draft: false
weight: 4
---

To keep it really simple, `.NET Core` code is divided into two bundling strategies:

**Projects** and **Solutions**

A `project` is a set of bundled source code files | defined by an `.csproj` file

A `solution` is a collection of projects and acts as a mediator between the projects it holds | defined by an `.sln` file

Here's a visual example:

```markdown
NeverendingTeaShop/
   src/
      NeverendingTeaShop.API
      NeverendingTeaShop.Application
      NeverendingTeaShop.Domain
      NeverendingTeaShop.Infrastructure
      NeverendingTeaShop.Persistence
   tests/
      NeverendingTeaShop.API.Tests
      NeverendingTeaShop.Application.Tests
      NeverendingTeaShop.Persistence.Tests
   NeverendingTeaShop.sln
```

The top level directory is a solution called **NeverendingTeaShop**,
defined by the existence of the file `NeverendingTeaShop.sln`.
`.sln` files are solution definition files auto-generated by the .NET Core CLI.

**NeverendingTeaShop** holds its source projects

- **NeverendingTeaShop.API** (template: webapi)
- **NeverendingTeaShop.Application** (template: classlib)
- **NeverendingTeaShop.Domain** (template: classlib)
- **NeverendingTeaShop.Infrastructure** (template: classlib)
- **NeverendingTeaShop.Persistence** (template: classlib)

and respective test projects (where all your test code lives)

- **NeverendingTeaShop.API.Tests** (template: xunit)
- **NeverendingTeaShop.Application.Tests** (template: xunit)
- **NeverendingTeaShop.Persistence.Tests** (template: xunit)

{{% notice info %}}
Test code is split from source code so there's no mixing of production artifacts
and test artifacts.
{{% /notice %}}

The above is an example of a clean architecture convention as created by a reference architecture found here:
[CleanArchitecture](https://github.com/ardalis/CleanArchitecture).

---

For more reading on clean architecture in .NET, take a look at:

https://github.com/dotnet-architecture
