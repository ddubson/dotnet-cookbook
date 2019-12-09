---
title: "Running tests locally"
date: 2019-10-06T13:36:15-04:00
draft: false
weight: 2
---

## Running all tests

```shell script
# from the base project directory
dotnet test
```

## Running a specific test project

```shell script
# from the base solution directory
dotnet test [test-project-path]

# from the test project directory
dotnet test

# e.g.
dotnet test tests/NeverendingTeaShop.API.Tests
```
