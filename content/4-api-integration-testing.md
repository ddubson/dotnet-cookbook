---
title: "Integration testing the REST API"
date: 2019-07-11T21:01:13-04:00
anchor: "api-integration-testing"
weight: 53
draft: true
---

In the spirit of Outside-In testing approach, let's start on the outer reaches of our application: an API integration test
suite. Let's imagine we had a prioritized backlog full of stories, with each story having a well-defined 
acceptance criteria about how our API should look like. Let's automate that acceptance criteria for this API!

In order to get started on testing our API routes, we have to be able to simulate our application, but we do not want 
to run it as a separate process that our test suite exercises. What we really want is for the test suite to create an 
application process, run the test cases, and teardown the application gracefully.

The package `Microsoft.AspNetCore.Mvc.Testing` is our friend here.

Let's add it to our test project:

{{<highlight bash>}}
dotnet add tests/WeatherStation.API.Tests package Microsoft.AspNetCore.Mvc.Testing
{{</highlight>}}

> The above command adds a library to your project. In .NET Core land, we call it a package, specifically a [NuGet package](https://docs.microsoft.com/en-us/nuget/what-is-nuget)
> which is a packaged piece of code (aka artifact) which is shared by the greater .NET community.

This testing package has all we need to run an application in-memory. It contains within it a test server that runs
beneath the hood, but let's not worry about that right now.
 
[TODO: continue on webapp factory + dependencies]


--

References

https://docs.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-2.2
https://fullstackmark.com/post/20/painless-integration-testing-with-aspnet-core-web-api
https://docs.microsoft.com/en-us/nuget/what-is-nuget



