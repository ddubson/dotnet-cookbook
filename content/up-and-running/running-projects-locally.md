---
title: "Running projects locally"
date: 2019-10-06T13:32:05-04:00
draft: false
weight: 1
---

Once a deployable project is [added](/creating-a-solution/adding-webapi-project),
you can run the project with .NET Core CLI

```shell script
# from the base project directory
dotnet run --project ./src/[project-path]

# OR from within the project directory
dotnet run

# e.g.
dotnet run --project ./src/GoodProduct.API
```
