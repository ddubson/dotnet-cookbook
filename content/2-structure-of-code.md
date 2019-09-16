---
title: "Structure of Code"
date: 2019-06-26T16:03:19-04:00
anchor: "structure-of-code"
weight: 51
---

To keep it really simple, `.NET Core` code is divided into two bundling strategies:

**Projects** and **Solutions**

A `project` is a set of bundled source code files.

A `solution` is a collection of projects and acts as a mediator between the projects it holds.

> It is important to note that you keep your tests separate from your actual production code.

Here's a visual example:

![solutions-and-projects](/images/solutions-and-projects.svg)

The **SoAwesomeSolution** is the main entity that holds the two source projects **SoAwesome.API** and **SoAwesome.Core**. It's an example of a clean architecture convention as created by [Ardalis](https://github.com/ardalis/CleanArchitecture). 

The test project **SoAwesome.Tests** holds all the tests for all projects, but in real life or when needed, this could be broken down to individual test projects for each source project.