---
title: "TravisCI"
date: 2019-10-16T14:39:21-04:00
draft: false
---

Below is an example of a simple build and test workflow for TravisCI.
To enable TravisCI, add a `.travis.yml` file in the solution root directory with the
following contents:

{{<highlight yml>}}
language: csharp
dist: xenial
addons:
  snaps:
    - name: dotnet-sdk
      classic: true
      channel: latest/beta
sudo: required
mono: none
solution: [solution-name].sln
script:
  - sudo snap alias dotnet-sdk.dotnet dotnet
  - dotnet test tests/[your-test-project]
  - dotnet test tests/[your-other-test-project]
{{</highlight>}}

{{% notice info %}}
There is currently a bug within TravisCI that will not allow `dotnet test`
to be run. The runtime hangs onto the process and the build times out. The
current workaround is to explicitly call `dotnet test` on specific test projects.
{{% /notice %}}

{{% notice warning %}}
The above TravisCI excerpt is subject to change as .NET Core 3.x is adopted
widely and some quirks in TravisCI configuration are removed and configuration is
simplified as time goes by.
{{% /notice %}}
