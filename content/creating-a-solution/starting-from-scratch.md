---
title: "Starting from scratch"
date: 2019-09-27T15:57:49-04:00
draft: false
weight: 1
---

{{%expand "TL;DR"%}}
```bash
# Create a solution
dotnet new sln --name [name-of-your-solution] --output [path-to-new-solution-on-file-system]
# Initialize the repo (once inside folder)
git init
# Fetch a standard C#/.NET .gitignore file
curl https://gitignore.io/api/visualstudio > .gitignore
# Fetch a standard C#/.NET .editorconfig file
curl https://gist.githubusercontent.com/ddubson/754257ef0b6037d2710b7750f0747ead/raw/513ef70ae856a4e5c30e5a4abd50c22c48d89d3f/.editorconfig > .editorconfig
```
{{%/expand%}}

## Prepare your machine

On a MacOs, to prepare your machine to be ready for .NET Core development, go get a really
great tool from Pivotal: [Workstation Setup](https://github.com/pivotal/workstation-setup)

```bash
git clone https://github.com/pivotal/workstation-setup
cd workstation-setup
chmod +x setup.sh

# Run the script that specifically downloads dotnet dependencies alongside common tooling
./setup.sh dotnet
```

{{% notice tip %}}
If you'd like a leaner install, refer [Installing the .NET Core SDK](/getting-started/installing-the-sdk)
section to get started.
{{% /notice %}}

## Creating a Solution

To create a new solution, use the .NET Core CLI to generate it:

```bash
dotnet new sln --name [name-of-your-solution] --output [path-to-new-solution-on-file-system]

# E.g.
dotnet new sln --name NeverendingTeaShop --output NeverendingTeaShop/
```

This command creates a new folder in the directory where you ran the command
with the given name that was passed in via the `output` flag.

## Initializing a Git repository

When navigating into the Solution folder, now is the optimal time to initialize the repository via

```bash
git init
```

## Create an ignore file

Now that your project is a Git tracked code base, let's make sure to create a `.gitignore` file specifically
tailored for .NET Core and C#.

Simply run the following:

```bash
curl https://gitignore.io/api/visualstudio > .gitignore
```

Alternatively, go to [gitignore.io](https://gitignore.io) and copy the `VisualStudio` ignore file and paste it into
an empty `.gitignore` within your Solution.

## Add an EditorConfig

EditorConfig configuration allows you to commit and track your code formatting style
of your project. It's important to make this decision early on (if you can!) of
how your code should format, so anyone who contributes knows exactly what
the formatting should be and the task of prettifying is left to the IDE.

Microsoft has published its own [example EditorConfig file for .NET projects](https://docs.microsoft.com/en-us/visualstudio/ide/editorconfig-code-style-settings-reference?view=vs-2019#example-editorconfig-file)

Create an `.editorconfig` file and run the following:

```bash
curl https://gist.githubusercontent.com/ddubson/754257ef0b6037d2710b7750f0747ead/raw/513ef70ae856a4e5c30e5a4abd50c22c48d89d3f/.editorconfig > .editorconfig
```
