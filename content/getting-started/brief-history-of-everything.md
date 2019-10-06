---
title: "Brief History of Everything"
date: 2019-09-25T09:02:55-04:00
draft: false
weight: 1
---

## .NET Core

.NET Core was introduced in 2014 as a response to the issue of a lack of unified framework contracts that can
be implemented across different platforms and devices, such as Windows Desktop, ASP.NET. Before .NET Core, each 
framework and platform was managed independently, with different release cadences, different supported platforms, etc.

Read more about .NET Core's origins -> [Introducing .NET Core](https://devblogs.microsoft.com/dotnet/introducing-net-core/)

## .NET Standard

The .NET Standard was introduced in 2016 as a unified collection of specifications that are tailored to have 
cross-platform implementations as described above. This allows us to use the same stack to develop for many 
different operating systems and devices.

Read more about .NET Standard's origins -> [Introducing .NET Standard](https://devblogs.microsoft.com/dotnet/introducing-net-standard/)

![.NET Standard overview](/images/NET-standard.png)

If you're wondering what should I use to build my application, start by asking what you want to build:

|I want to build...|then I'll use...|
|------------------|----------------|
|an MVC web app         |[.NET Core]((https://docs.microsoft.com/en-us/dotnet/core/))|
|an web api             |[.NET Core]((https://docs.microsoft.com/en-us/dotnet/core/))|
|a native Windows app   |[.NET Framework](https://dotnet.microsoft.com/download/dotnet-framework)|
|a mobile Android app   |[Xamarin.Android](https://docs.microsoft.com/en-us/xamarin/android/index)|
|a mobile iOS app       |[Xamarin.iOS](https://docs.microsoft.com/en-us/xamarin/ios/index)|

All the above frameworks and runtimes adhere to the .NET Standard
