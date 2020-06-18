---
title: "Handling HTTP Request/Response bodies"
date: 2020-06-18T12:34:29-04:00
draft: false
weight: 2
---

When working with functional (e.g. API) tests in your project, you might be in
need of serializing a request body to JSON and deserializing a response body
from JSON on the response of the HTTP client in your test case.

Here's a few pre-packaged generic functions that can help reduce boilerplate:

```csharp
public static StringContent CreateRequestBody<T>(T t) => new StringContent(JsonConvert.SerializeObject(t), Encoding.UTF8, "application/json");

public static T ReadResponseBody<T>(string responseBody) => JsonConvert.DeserializeObject<T>(responseBody);
```

Here's an example of how they can be used in a functional test:

```csharp
// Using xUnit and FluentAssertions

[Fact]
public async Task Create_project_yields_created_project()
{
    using var server = CreateServer();
    var requestBody = CreateRequestBody(new ProjectDto {Name = "Project created by a test case"});
    var response = await server.CreateClient().PostAsync(Post.Projects, requestBody);

    response.StatusCode.Should().Be(HttpStatusCode.Created);
    var responseBody = ReadResponseBody<Project>(await response.Content.ReadAsStringAsync());
    responseBody.Id.Should().NotBe(null);
    responseBody.Name.Should().Be("Project created by a test case");
}
```
