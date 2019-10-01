# Simple C# Web Server

## Startup Steps
- Open a terminal and change to the folder containing the project. Specifically, where the `.sln` file is

## Build the app
- `dotnet build`

## Starting the server
- `dotnet run --project basic-web-app`

## Testing
- Run the tests
  - `dotnet test`

___________

# C# AWS codepipeline deployment
## Foreword
This document will focus on following the aws tutorial as closely as possible while modifying the information to relate to a C#/.NET 
This guide will use the following information...
- [aws codepipeline tutorial - https://aws.amazon.com/getting-started/tutorials/continuous-deployment-pipeline/](https://aws.amazon.com/getting-started/tutorials/continuous-deployment-pipeline/)
- [C# WebApp - https://github.com/codefellows/deployment-app-csharp](https://github.com/codefellows/deployment-app-csharp)
## How to Deploy a C# App with AWS Codepipeline
1. Create an AWS ElasticBeanstalk environment. (This will take a several minutes.) 
![envStep1 HERE](/assets/envStep1.png)
2. Fork the C# repository to your own account that will be able to commit changes to the repository.
![PictureOfForking HERE](/assets/forkImg.png)
3. Verify that the application has a buildspec.yml file that contains the following at the root level...
**buildspec.yml**
```
version: 0.2

phases:
  install:
    runtime-versions:
       dotnet: 2.2
  build:
    commands:
      - dotnet restore basic-web-app/basic-web-app.csproj
      - dotnet build basic-web-app/basic-web-app.csproj
      - dotnet publish basic-web-app/basic-web-app.csproj -o site
artifacts:
  files:
    - basic-web-app/site/**/*
    - basic-web-app/site/aws-windows-deployment-manifest.json
```
Note: The buildspec.yml will be required to include the phases with the runtime version.

4. Start creating the codepipeline... 
  * Create your pipeline
  ![Start series of instructions here](/assets/pipelinestep3.png)
  ![step 3b](/assets/pipeline3b.png)
  * Connect with your GitHub repository
  ![step 3c](/assets/pipeline3c.png)
  ![step 3c-2](/assets/pipeline3c-2.png)

  * Set up the build
  ![settings](/assets/build-settings.png)
  ![yml](/assets/build-config.png)

  * Success!
  ![success](/assets/pipeline-success.png)



