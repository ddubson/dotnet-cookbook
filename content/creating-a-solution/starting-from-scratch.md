---
title: "Starting from scratch"
date: 2019-09-27T15:57:49-04:00
draft: false
weight: 1
---

## Creating a Solution

To create a new solution, use the .NET Core CLI to generate it:

```bash
dotnet new sln --name [name-of-your-solution] --output [path-to-new-solution-on-file-system]

# E.g.
dotnet new sln --name GoodProduct --output GoodProduct/
```

This command creates a new folder in the directory where you ran the command with the given name that was passed in
via the `output` flag.

## Initializing a Git repository

When navigating into the Solution folder, now is the optimal time to initialize the repository via

```bash
git init
```

### Create an ignore file

Now that your project is a Git tracked code base, let's make sure to create a `.gitignore` file specifically
tailored for .NET Core and C#.

Simply run the following:

```bash
curl https://gitignore.io/api/visualstudio > .gitignore
```

Alternatively, go to [gitignore.io](https://gitignore.io) and copy the `VisualStudio` ignore file and paste it into
an empty `.gitignore` within your Solution.





