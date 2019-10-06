---
title: "Running projects locally"
date: 2019-10-06T13:32:05-04:00
draft: true
weight: 4
---

Once a Web API project is [added](/creating-a-solution/adding-projects),
you can run the project with .NET Core CLI

```shell script
# from the base project directory
dotnet run --project ./src/[project-path]

# from within the project directory
dotnet run

# e.g.
dotnet run --project ./src/GoodProduct.API
```

