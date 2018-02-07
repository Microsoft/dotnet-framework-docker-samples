# .NET Framework 4.7.1 Console Sample

This .NET Framework Docker sample demonstrates a best practice pattern for building Docker images for .NET Framework apps. It shows you how you can build and run the app using Docker. 

The [sample Dockerfile](Dockerfile) creates a .NET Framework 4.7.1 application Docker image based off of the [.NET Framework Runtime Docker base image](https://hub.docker.com/r/microsoft/dotnet-framework/). A nearly identical sample is available for [.NET Framework 3.5](../dotnetapp-3.5/README.md).

It uses the [Docker multi-stage build](https://github.com/dotnet/announcements/issues/18) feature to build the sample in a container based on the larger [.NET Framework build base image](https://hub.docker.com/r/microsoft/dotnet-framework-build/) and then copies the final build result into a Docker image based on the smaller [.NET Framework runtime base image](https://hub.docker.com/r/microsoft/dotnet-framework/). The build image contains tools that are required to build applications while the runtime image does not.

This sample requires [Docker 17.10](https://docs.docker.com/release-notes/docker-ce) or later of the [Docker client](https://www.docker.com/community-edition). You need the latest Windows 10 or Windows Server 2016 to use Windows containers. The instructions assume you have the Git client installed.

## Getting the sample

The easiest way to get the sample is by cloning this repository with git, using the following instructions.

```console
git clone https://github.com/Microsoft/dotnet-framework-docker-samples
```

You can also [download the repository as a zip](https://github.com/Microsoft/dotnet-framework-docker-samples/archive/master.zip).

## Build and run the sample with Docker

You can build and run the sample in Docker using the following commands. The instructions assume that you are in the root of the repository.

```console
cd dotnetapp
docker build -t dotnetapp .
docker run --rm dotnetapp Hello .NET Framework from Docker
```

Note: The instructions above work on multiple versions of Windows. The .NET Framework base images use [multi-arch tags](https://github.com/dotnet/announcements/issues/14), which are used to abstract away [different versions of Windows base images](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/version-compatibility). This means that you will get different results depending on the version of Windows that you are using.

## Build and run the sample locally with MSBuild

You can build and run the sample locally with MSBuild using the following instructions. The instructions assume that you have [Visual Studio 2017](https://www.visualstudio.com/) installed, that you are using the `Developer Command Prompt for VS 2017`, and  that you are in the root of the repository.

```console
cd dotnetapp
msbuild.exe /t:restore
msbuild.exe /t:Build /p:Configuration=Release /p:OutputPath=out
```

You can run the application using the following command.

```console
out\dotnetapp.exe
```

## Build and run the sample locally with the .NET Core SDK

You can build and run the sample locally with the [.NET Core 2.0 SDK](https://www.microsoft.com/net/download/core) using the following instructions. The instructions assume that you are in the root of the repository.

```console
cd dotnetapp
dotnet run Hello .NET Framework
```

You can produce an application that is ready to deploy to production locally using the following command.

```console
dotnet publish -c release -o out
```

You can run the application using the following command.

```console
out\dotnetapp.exe
```

## Docker Images used in this sample

The following Docker images are used in this sample

* [microsoft/dotnet-framework-build:4.7.1](https://hub.docker.com/r/microsoft/dotnet-framework-build)
* [microsoft/dotnet-framework:4.7.1](https://hub.docker.com/r/microsoft/dotnet-framework)

## Related Resources

* [ASP.NET Docker sample](../aspnetapp/README.md)
* [.NET Framework Docker samples](../README.md)
* [.NET Core Docker samples](https://github.com/dotnet/dotnet-docker-samples)