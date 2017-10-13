# Lift & Shift Sample for ASP.NET 4.x

Running an existing .NET Framework-based application in a Windows container
requires creating the Docker image that contains your application, and
starting one or more containers to run that image. This topic explains
the tasks you must perform to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.

## Prerequisites

At a minimum, your development machine must be running
[Windows 10 Anniversary Update](https://www.microsoft.com/en-us/software-download/windows10/)
or [Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server) and you need to install [Docker for Windows](https://docs.docker.com/docker-for-windows/).

After installing and starting Docker, you'll need to right-click on the
tray icon and select **Switch to Windows containers** in order to run
Docker images based on Windows.

## Visual Studio 2017

[Visual Studio 2017](https://www.visualstudio.com/downloads) is the required version to support adding Docker support for ASP.NET 4.x applications.

### Adding Docker Support

Right click the project, select **Add -> Docker Support**.

A new project type **.dcproj** is added with the Docker files for building, debugging and publishing the image.

**Dockerfile**

The base image used is `microsoft/aspnet:4.7` which includes `microsoft/iis`.

```dockerfile
FROM microsoft/aspnet:4.7
ARG source
WORKDIR /inetpub/wwwroot
COPY ${source:-obj/Docker/publish} .
```

Start the application by clicking the **Docker** from the Debug menu; starting the application in a container and attaching the debugger allowing for you to debug your ASP.NET code *inside* the container.

### Publishing your application

Just as you would publish your application using the publish wizard, now you can publish your container images to Docker Hub, Azure Container Registry or Azure App Service through the same publishing wizard.