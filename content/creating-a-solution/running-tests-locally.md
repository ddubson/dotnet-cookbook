---
title: "Running tests locally"
date: 2019-10-06T13:36:15-04:00
draft: true
weight: 5
---

## Running all tests

```shell script
# from the base project directory
dotnet test
```

## Running a specific test project

```shell script
# from the base directory directory
dotnet test [test-project-path]

# from the test project directory
dotnet test

# e.g.
dotnet test tests/GoodProduct.API.Tests
```
