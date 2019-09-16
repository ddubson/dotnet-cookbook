---
title: "Creating a REST API with .NET Core"
date: 2019-06-23T19:54:54-04:00
anchor: "creating-an-api-with-dotnet-core"
weight: 52
---

Let's build a REST API. 

As an example, we'll build a weather service that will give us some real interesting facts about current weather conditions in the world.

.NET Core CLI has a concept of **templates** which we'll be using to generate projects within a solution.

{{<highlight bash>}}
# Create a directory and navigate to it
mkdir dotnet-weather-station
cd dotnet-weather-station

# Make this directory our 'solution' with the name WeatherStation
dotnet new sln --name WeatherStation

# Let's take a look at the selection of templates .NET Core provides
dotnet new --list

# The closest option for our use case is the webapi option (shorthand)
# Create an API project using the webapi template
dotnet new webapi --output src/WeatherStation.API --name WeatherStation.API

# Clean up unnecessary auto-generated controllers
rm -rf src/WeatherStation.API/Controllers

# Create an accompanying test project using xUnit which will hold all the API test cases
dotnet new xunit --output tests/WeatherStation.API.Tests --name WeatherStation.API.Tests

# Clean up unnecessary auto-generated test cases
rm tests/WeatherStation.API.Tests/UnitTest1.cs

# Add the WeatherStation.API project reference to the test project
dotnet add tests/WeatherStation.API.Tests reference src/WeatherStation.API/WeatherStation.API.csproj

# Add the newly created API project and test API project to be part of the 'solution'
dotnet sln WeatherStation.sln add src/WeatherStation.API/WeatherStation.API.csproj
dotnet sln WeatherStation.sln add src/WeatherStation.API.Tests/WeatherStation.API.Tests.csproj
{{</highlight>}}

At this point, we can import the project into JetBrains Rider IDE by opening a solution that we have just
created.

The structure of our directory tree should look similar to below. Let's take this opportunity to 
describe what solution (.sln) and project (.csproj) do.

![Directory structure - New solution](/images/directory-structure-new-solution.svg)

It's important to note that all the projects in the `tests` directory are never packaged as part of the runtime executable.

---

## Create the first controller

Within `src/WeatherStation.API` project, create a `WeatherStationIntroController.cs` file.

`*.cs` files are C# files. Here's the contents for our first controller:

{{<highlight csharp>}}
using Microsoft.AspNetCore.Mvc;

namespace WeatherStation.API
{
    [Route("/")]
    public class WeatherStationIntroController : ControllerBase
    {
        [HttpGet]
        public string WeatherStationIntroduction() => "This is the weather station.";
    }
}
{{</highlight>}}

Let's take a moment to break down the contents of this first Controller class.

![First controller](/images/first-controller.svg)

## Run the API project locally

To start the REST API project locally, run...

{{<highlight bash>}}
dotnet run --project src/WeatherStation.API
{{</highlight>}}

You should see it bind to ports `5000` (http) and `5001` (https) by default.

Here's an example log output

{{<highlight bash>}}
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\..\AppData\Local\ASP.NET\DataProtection-Keys'
      as key repository and Windows DPAPI to encrypt keys at rest.
Hosting environment: Development
Content root path: G:\workspace\dotnet-weather-station\src\WeatherStation.API
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
{{</highlight>}}

Use Google Chrome browser to navigate to `http://localhost:5000`. It will redirect you to `https://localhost:5001`, proceed with accepting the risk of a self-signed certificate and you should see the output of the root route we described above.