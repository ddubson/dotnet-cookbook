---
title: "Deploying to Pivotal Platform"
date: 2019-11-14T13:58:52-05:00
draft: false
tags: ["pivotal platform", "deploy", "cloud foundry", "publishing"]
---

To deploy to Pivotal Platform, a few steps have to be taken as described below.

## Steps at a glance

{{<mermaid>}}
graph LR;
    id1(Install CloudFoundry CLI)-->id2(Build and package your application)
    id2-->id3(Create a CF manifest)
    id3-->id4(Log in to a CF API)
    id4-->id5(Push your application)
{{</mermaid>}}

## Download and install the CloudFoundry CLI

On MacOS, the simplest way to get the CLI is via Homebrew:

```bash
brew install cloudfoundry/tap/cf-cli
```

For further information, check out the [CF CLI Downloads Section](https://github.com/cloudfoundry/cli#downloads)

## Build the application

Before we can deploy to Pivotal Platform, we'll have to build and package our application

Here's an opinionated example of doing so:

```bash
dotnet publish ./path/to/your/myproject.csproj --configuration Release

# e.g.
dotnet publish ./src/NeverendingTeaShop.API/NeverendingTeaShop.API.csproj --configuration Release
```

{{% notice info %}}
The `--configuration Release` flag describes type of configuration to enable in .NET. Read more about the `publish`
command and configurations [here](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish)
{{% /notice %}}

The `publish` command should now have created a directory structure in the project you wanted to build:

```bash
myproject/bin/Release/netcoreapp3.0/publish

e.g.
./NeverendingTeaShop/src/NeverendingTeaShop.API/bin/Release/netcoreapp3.0/publish
```

## Create a CF Manifest

Pivotal Platform uses manifest files to understand what type of application you are deploying and what the
parameters are for when the application is deployed (such as allocated memory and disk space).

In addition, Pivotal Platform relies on a concept of a buildpack to construct a relevant environment in the cloud
for your application.

We'll be using the [.NET Core Buildpack](https://docs.cloudfoundry.org/buildpacks/dotnet-core/index.html)

The manifest file (`manifest.yml`) should be placed in the root of your project for ease of navigation to subdirectories.

Here's an example manifest file:

```yaml

---
applications:
  - name: NeverendingTeaShopAPI
    path: src/NeverendingTeaShop.API/bin/Release/netcoreapp3.0/publish
    memory: 1G
    disk_quota: 512M
    env:
      ASPNETCORE_Environment: staging
    buildpacks:
       - https://github.com/cloudfoundry/dotnet-core-buildpack.git

```

Quick breakdown of each field in the example manifest:

- `name` - describes the name of your application. This will be the name of the application in Pivotal Platform
- `path` - the path to your compiled artifacts directory. For .NET Core 3.0, this path is likely to be
`bin/Release/netcoreapp3.0/publish`. **Important to note that this path is relative to the manifest file location**.
- `memory` - descriptor of how much RAM to allocate to the container running your application in the cloud
- `disk_quota` - descriptor of how much disk space to allocate to the container running your application in the cloud
- `env` - array of environment variables to deploy your container with. This is useful to describe deployment parameters
DO NOT use this for passwords or any other type of secrets.
- `buildpacks` - an array of buildpacks to include in the container deploying your application.

## Log in to a CF API

In order to deploy applications to Pivotal Platform, we'll need a place to deploy them to.

In this example, I'll be using an account on Pivotal Web Services that I have created. To create your own,
go to [Pivotal Web Services](https://run.pivotal.io)

Using the CF CLI,

```bash
cf login -a https://api.run.pivotal.io

# If using a single-sign on address
cf login -a https://api.run.pivotal.io --sso
```

This command should prompt you to enter username and password, your organization and space (concepts beyond the scope
of this tutorial).

## Push your application

When everything is gathered together, all that's left is to deploy:

```bash
# Default deploy, looks for manifest.yml in the same directory as command being run
cf push

# OR with specific include of the manifest being used
cf push -f manifest.yml
```

---

If you're **stuck** (read: something isn't going right with this process), take a look at the
[example project](https://github.com/ddubson/NeverendingTeaShop/blob/master/manifest.yml).
