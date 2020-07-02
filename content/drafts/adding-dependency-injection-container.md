---
title: "Adding Dependency Injection Container (Autofac)"
date: 2020-06-19T17:58:03-04:00
draft: true
---

Guide based on Autofac 6.0.0

- Add Autofac nuget (Autofac.Extensions.DependencyInjection)
- Register service provider factory in host builder (Program.cs usually)
- Create a module class, extending Module from Autofac lib
	- How do I think about creating modules
- In startup.cs, register the module within ConfigureContainer convention method

Configure for a functional test suite

- Create a test server (host builder) and a test startup
- Include service provider factory to be autofac
- If need to create a test module, in test startup, create a specific environment name, apply it
- Create a convention override in test startup.cs like `ConfigureFunctionalTestsContainer`
and register a test application module.