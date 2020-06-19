---
title: "Customizing Startup Behavior"
date: 2020-06-19T17:57:39-04:00
draft: false
weight: 3
tags: ['startup', 'customizing', 'configure', 'dependency-injection', 'magic', 'convention']
---

{{% notice info %}}
This guide is for .NET Core 3.1+, some examples are not backwards compatible
{{% /notice %}}

In .NET Core web projects, the `Startup` class is your application's primary runtime configuration class. Here, the services that your app needs will be wired up together, and additional configuration options will be set for your app to run smoothly.

At first, you might be perfectly content with the default runtime configuration,
but as soon as you start adding more and more logic into your app, you'll start
to wonder

- How do I register runtime objects into a Dependency Injection (DI) container?
- How do I enable configurations for specific environments?
- How do I toggle the security layer around my application?
- How do I create a "test" mode for my functional/integration tests?

The `Startup` class is a bit magical -- in that the designers of this class
made some decisions for it to be quite customizable but only if you know how to
customize it. The class does not inherit any other class, but is registered by
the WebHostBuilder as the primary Startup class.

The primary methods the class has start with `Configure...`, such as

- `ConfigureServices` - default method to wire up services in your application
- `ConfigureContainer` - default method to wire up a DI container
- `Configure` - default method to enable/disable application flags, security, etc.
- Create your own!
  - `Configure[EnvironmentName]Services` - specific method to wire up services only in `[EnvironmentName]` (e.g. `Development`, `Production`, `FunctionalTests`, etc.)
  - `Configure[EnvironmentName]Container` - environment specific DI container configuration method
  - `Configure[EnvironmentName]` - environment specific app configuration method

The startup class can have multiple methods prefixed with `Configure...`, and you
can create your own variations.

Here's an example Startup

```csharp
public class Startup {
  // This is the default if you don't have an environment specific method.
  public void ConfigureServices(IServiceCollection services)
  {
    // Add things to the service collection.
  }

  // This only gets called if your environment is Development. The
  // default ConfigureServices won't be automatically called if this
  // one is called.
  public void ConfigureDevelopmentServices(IServiceCollection services)
  {
    // Add things to the service collection that are only for the
    // development environment.
  }

  // This is the default if you don't have an environment specific method.
  public void ConfigureContainer(ContainerBuilder builder)
  {
    // Add things to the DI ContainerBuilder.
  }

  // This only gets called if your environment is Production. The
  // default ConfigureContainer won't be automatically called if this
  // one is called.
  public void ConfigureProductionContainer(ContainerBuilder builder)
  {
    // Add things to the ContainerBuilder that are only for the
    // production environment.
  }

  // This is the default if you don't have an environment specific method.
  public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
  {
    // Set up the application.
  }

  // This only gets called if your environment is Staging. The
  // default Configure won't be automatically called if this one is called.
  public void ConfigureStaging(IApplicationBuilder app, ILoggerFactory loggerFactory)
  {
    // Set up the application for staging.
  }
}
```

This example is [referenced from Autofac DI docs](https://autofaccn.readthedocs.io/en/latest/integration/aspnetcore.html#quick-start)

Here's a customized `Startup` class that enables a database context when running
with `EnvironmentName=Development`

```csharp {linenos=table,hl_lines=["15-19"]}
public class Startup {
  public Startup(IConfiguration configuration)
  {
      Configuration = configuration;
  }

  public IConfiguration Configuration { get; }

  public void ConfigureServices(IServiceCollection services)
  {
      services.AddControllers();
  }

  // This runs only for "Development" environment (ASPNETCORE_ENVIRONMENT)
  public void ConfigureDevelopmentServices(IServiceCollection services)
  {
      ConfigureServices(services);
      services.AddScoped(options => new ContextFactory().CreateDbContext(null!));
  }

  // Executed in any environment and creates a DI container
  public void ConfigureContainer(ContainerBuilder containerBuilder)
  {
      // This wires up Autofac module; more on this in another post
      containerBuilder.RegisterModule(new ApplicationModule());
  }

  // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
  public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
  {
      if (env.IsDevelopment())
      {
          app.UseDeveloperExceptionPage();
      }

      app.UseHttpsRedirection();
      app.UseRouting();

      ConfigureAuth(app);

      app.UseEndpoints(endpoints =>
      {
          endpoints.MapControllers();
      });
  }
}
```
