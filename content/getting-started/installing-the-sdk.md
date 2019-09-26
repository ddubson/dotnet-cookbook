---
title: "Installing the .NET Core SDK"
date: 2019-09-16T13:04:55-04:00
draft: false
weight: 2
---

The first step is to download and install the `.NET Core SDK`. 
This is the development kit for .NET that will be the engine for your application.

> If you're familiar with Java, `.NET Core SDK` is similar to `Oracle JDK`, `OpenJDK`, or the 
> other billion JDK variants.

## MacOS

### Using Homebrew

The simplest way to obtain the .NET Core SDK on a Mac is through [Homebrew](https://brew.sh). 
Once you've downloaded and installed Homebrew, run the following command in your Terminal:

```bash
brew cask install dotnet-sdk
```

Once installed, if you want to verify the installation, run:

```bash
dotnet --version
```

> .NET Core SDK comes bundled with the .NET Core CLI, in the form of `dotnet` command.

#### Debugging Support

To be able to run a debugger on your code, you have to install the Mono project, a cross-platform implementation 
of the .NET Standard:

```bash
brew install mono
```

### Downloading directly

Navigate to <a href="https://dotnet.microsoft.com/download" target="_blank">Microsoft .NET Core downloads page</a> 
and install the MacOS version of the latest .NET Core SDK.

 
