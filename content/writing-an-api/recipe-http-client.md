---
title: "Saving HTTP requests"
date: 2020-06-13T16:47:03-04:00
draft: false
weight: 2
tags: ['http', 'recipe']
---

> This recipe is only if you are using a JetBrains product as your IDE

When just starting out writing an API, you might write a little of the API code
and test that the API works by placing a request via Postman or Insomnia HTTP
clients manually, if not writing tests first.

A better approach to track all the requests that can be made via the API is
to create and git track an `*.http` file. In JetBrains Rider (and other JetBrains
IDEs), http files can be executed in place, so you're able to write requests
and save them for later.

Here's an example `api.http`:

```http
GET {{host}}/api/projects

GET {{host}}/api/projects/1
```

An adjoining `http-client-env.json` next to the http file can be used to denote
an environment to run the http requests against. That is what the `{{host}}`
placeholder is for.

An example of an `http-client-env.json` file:

```json
{
  "local": {
    "host": "http://localhost:5000"
  },
  "dev": {
    "host": "some-remote-address"
  }
}
```

## Highlights

- You can save and track all types of HTTP requests and payloads.
- Each of the requests can be executed separately.
- Requests can be piped from one to another.

[Learn more about Http client](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html)
