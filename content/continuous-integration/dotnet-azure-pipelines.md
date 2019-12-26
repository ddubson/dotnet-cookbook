---
title: "Azure Pipelines"
date: 2019-07-12T13:12:54-04:00
draft: false
weight: 2
---

This guide will help you understand what is involved in building a .NET Core
application, and deploying that application continuously to Azure App services.

**[Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/)**
within Azure DevOps portal is Microsoft's CI/CD solution.

The fundamental artifact involved in setting up a CI/CD pipeline with Azure Pipelines
is the `azure-pipelines.yml` file that you'll need to create in the root directory
of your repository.

Login to your Azure DevOps portal and execute the following steps to create a
pipeline. If you already have a pipeline, you can skip this set of steps.

1. Navigate to [Azure Pipelines Dashboard](https://dev.azure.com)
2. Log in and create a new pipeline.
3. Go to **Pipelines -> Builds -> New Build Pipeline**
4. Go through the wizard: **Connect to GitHub Yaml -> Select Repo -> ASP.NET Core Project -> Review**
5. On Review stage, refer to the Yaml below for how to approach creating a
build artifact for a .NET Core application.

The semi-automated wizard will provide you with a default `azure-pipelines.yml`
file template. Use this as a starting point and place it in your root directory
of your git repository.

An example of an `azure-pipelines.yml` can be found below, but before exploring
that, let's look at the steps involved at a glance.

{{<mermaid>}}
graph TD;
    id1("[Job1] Run tests")-->id2("[Job2] Build application")
    id2-->id3("[Job2] Copy build artifacts to artifacts directory")
    id3-->id4("[Job2] Publish artifacts directory to central location as artifact")
    id4-->idx("Artifact store (accessible between jobs)")
    idx-->id5("[Job3] Download artifact from central location")
    id5-->id6("[Job3] Use Azure Resource Manager to publish artifact to Azure App Services")
    style idx fill:lightgreen,stroke:#333
{{</mermaid>}}

Your `azure-pipelines.yml` should look similar to the below example:

{{<highlight yaml>}}
# ASP.NET Core
# Build and test ASP.NET Core projects targeting .NET Core.
# Add steps that run tests, create a NuGet package, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/languages/dotnet-core

trigger:
- master

pool:
  vmImage: 'ubuntu-latest'

variables:
  buildConfiguration: 'Release'
  AzureSubscriptionServiceConnectionName: 'CHANGEME'
  AzureResourceGroup: 'CHANGEME'
  AzureWebAppServiceName: 'CHANGEME'

stages:
  stage: MyPipeline
  jobs:
    - job: TestApp
      dependsOn: []
      displayName: "Run tests"
    - job: BuildApp
      dependsOn: TestApp
      displayName: "Build application"
      steps:
        - bash: dotnet build -c $(buildConfiguration) --output artifacts/
        - task: CopyFiles@2
          displayName: 'Copy build artifacts to Artifacts Directory'
          inputs:
            SourceFolder: '$(Build.SourcesDirectory)/artifacts'
            Contents: |
              **/*
            TargetFolder: '$(Build.ArtifactStagingDirectory)'
        - task: PublishBuildArtifacts@1
          displayName: 'Publish build artifacts to central location'
          inputs:
            pathToPublish: '$(Build.ArtifactStagingDirectory)'
            artifactName: myArtifacts
    - deployment: DeployApp
      displayName: "Deploy application"
      dependsOn: BuildApp
      environment: 'MyAppDevEnvironment'
      strategy:
        runOnce:
          deploy:
            steps:
              - task: DownloadBuildArtifacts@0
                inputs:
                  buildType: 'current'
                  downloadType: 'single'
                  artifactName: 'myArtifacts'
                  downloadPath: '$(System.ArtifactsDirectory)'
              - task: AzureRMWebAppDeployment@4
                displayName: Azure App Service Deploy
                inputs:
                  appType: webApp
                  ConnectedServiceName: $(AzureSubscriptionServiceConnectionName)
                  ResourceGroupName: $(AzureResourceGroup)
                  WebAppName: $(AzureWebAppServiceName)
                  Package: '$(System.ArtifactsDirectory)/myArtifacts'
{{</highlight>}}

The above example is based on an `ubuntu-latest` image that Microsoft provides
as the base of CI operations. [What's included in the image can be found here](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/hosted?view=azure-devops)
