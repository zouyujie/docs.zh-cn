---
title: "将 ASP.NET MVC 应用程序迁移到 Windows 容器"
description: "了解如何利用现有 ASP.NET MVC 应用程序并在 Windows Docker 容器中运行它"
keywords: "Windows 容器, Docker, ASP.NET MVC"
author: BillWagner
manager: wpickett
ms.date: 09/28/2016
ms.topic: article
ms.prod: .net-framework-4.6
ms.technology: dotnet-mvc
ms.devlang: dotnet
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
translationtype: Human Translation
ms.sourcegitcommit: 15c55a87beb64f265a164db918c7721c7690fadf
ms.openlocfilehash: bde267042883d2f25848747047845a16b181e549

---

# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>将 ASP.NET MVC 应用程序迁移到 Windows 容器

要在 Windows 容器中运行基于 .NET Framework 的现有应用程序，需要创建包含应用程序的 Docker 映像，然后启动一个或多个容器运行该映像。 本主题介绍利用现有 [ASP.NET MVC 应用程序](http://www.asp.net/mvc)并在 Windows 容器中部署它需要执行的任务。

先以现有 ASP.NET MVC 应用程序开始。 然后，使用 Visual Studio 生成已发布资产。 使用 Docker 创建包含应用程序的映像，并在映像启动时运行该应用程序。 完成后便可以将浏览器连接到在 Windows 容器中运行的站点，然后验证应用程序是否正在运行。

本文可确保基本了解 Docker。 有关 Docker 体系结构的详细信息，请参阅 Docker 站点上的 [Docker 概述](https://docs.docker.com/engine/understanding-docker/)（如果这些概念是全新概念）。

要在容器中运行的应用程序是一个随机回答问题的简单网站。 此应用程序是一款不具备身份验证支持或数据库存储的基本 MVC 应用程序，让用户可以专注于将 Web 层移动到容器。 后续主题将演示如何在容器化应用程序中移动和管理永久性存储。

移动应用程序涉及以下步骤：

1. [创建发布任务以生成映像资产。](#publish-script)
2. [生成将运行应用程序的 Docker 映像。](#build-the-image)
3. [启动用于运行映像的 Docker 容器。](#start-a-container)
4. [使用浏览器验证应用程序。](#verify-in-the-browser)

完成的应用程序位于 [GitHub 上的 dotnet/core-docs 存储库](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator)。

## <a name="prerequisites"></a>先决条件

开发计算机最低需运行 [Windows 10 周年更新](https://www.microsoft.com/en-us/software-download/windows10/) 或 [Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server)。 

开始之前，需要安装 [Docker for Windows](https://docs.docker.com/docker-for-windows/) 1.12 Beta 26 版或更高版本。 此次，Windows 容器支持仅在 Beta 通道中可用。

> [!IMPORTANT]
> 如果正使用的是 Windows Server 2016，需先按照[容器主机部署 - Windows Server](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/deployment/deployment)中的说明操作才能运行 Docker 容器。

安装并启动 Docker 后，需要右键单击托盘图标并选择“切换到 Windows 容器”才能基于 Windows 运行 Docker 映像。 此命令需要几秒钟执行：

![Windows 容器][windows-container]

## <a name="publish-script"></a>发布脚本

第一步是获取需要加载到同一位置中 Docker 映像中的所有资产。 幸运地是，可以使用 Visual Studio 的“发布”命令来创建应用程序的发布配置文件。 此配置文件会将所有资产置于同一目录树中，本教程后面会将该目录树复制到目标映像。

**发布步骤**

1. 在 Visual Studio 中右键单击 Web 项目，然后选择“发布”。
2. 单击“自定义配置文件”按钮，然后选择“文件系统”作为方法。
3. 选择该目录。 按照约定，已下载示例将使用 `bin/PublishOutput`。

![发布连接][publish-connection]

接下来，打开“设置”选项卡上的“文件发布选项”部分。 选择“在发布期间预编译”。 这种优化意味着在 Docker 容器中编译视图的同时也将复制该预编译视图。

![发布设置][publish-settings]

单击“发布”，Visual Studio 会将所有所需资产复制到目标文件夹。 

## <a name="build-the-image"></a>生成映像

在 Dockerfile 中定义 Docker 映像，Dockerfile 包含有关基本映像、任何其他组件、要运行的应用程序和其他配置映像的说明。  Dockerfile 是用于创建该映像的 `docker build` 命令的输入。

根据位于 [Docker 中心](https://hub.docker.com/r/microsoft/aspnet/) 的 `microsft/aspnet` 映像生成映像。
基本映像 `microsoft/aspnet` 为 Windows Server 映像。 除 Windows Server Core 外，还安装并启用了 IIS 和 ASP.NET 4.6.2。 在容器中运行此映像时，它将自动启动 IIS，任何已安装的网站也将处于活动状态。

创建映像的 Dockerfile 如下所示：

```
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# Next, this Dockerfile creates a directory for your application
RUN mkdir C:\randomanswers

# configure the new site in IIS.
RUN powershell -NoProfile -Command \
    Import-module IISAdministration; \
    New-IISSite -Name "ASPNET" -PhysicalPath C:\randomanswers -BindingInformation "*:8000:"

# This instruction tells the container to listen on port 8000. 
EXPOSE 8000

# The final instruction copies the site you published earlier into the container.
ADD containerImage/ /randomanswers
```

此 Dockerfile 中不含 `ENTRYPOINT` 命令。 不需要该命令。
基本映像可确保容器启动时 IIS 也随之启动。 

接下来，需要运行 Docker 生成命令，创建用于运行 ASP.NET 应用程序的映像。 为此，请打开 PowerShell 窗口，然后在解决方案目录中键入以下命令：

```
docker build -t mvcrandomanswers .
```

此命令将按照 Dockerfile 中的说明生成新映像。 这可能包括从 [Docker 中心](http://hub.docker.com)拉取基本映像，然后命令会将应用程序添加到该映像。

命令完成后，便可以运行 `docker images` 命令，查看有关新映像的信息：

```
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       8.104 GB
```

计算机上的 IMAGE ID 会所不同。 现在，运行应用程序。

## <a name="start-a-container"></a>启动容器

通过执行以下 `docker run` 命令来启动容器：

```
docker run -d -p 8000:8000 --name randomanswers mvcrandomanswers
```

`-d` 参数告知 Docker 在分离模式下启动映像。 这意味着 Docker 映像会以断开连接当前 shell 的状态运行。

`-p 8000:8000` 参数告知 Docker 如何映射传入端口。 在此示例中，在主机和容器上使用的都是端口 8000。

`--name randomanswers` 为运行中容器命名。 可在大多数命令中使用此名称，而不是容器 ID。

`mvcrandomanswers` 是要启动的映像名称。

## <a name="verify-in-the-browser"></a>在浏览器中验证

> [!NOTE]
> 借助当前版本，无法使用 `http://localhost` 浏览到站点。 这是由于 WinNAT 中某已知行为的原因，后续版本将解决此问题。 问题得到解决前，需要使用容器的 IP 地址。

启动容器后，需要查找其 IP 地址，以便可从浏览器连接到正在运行的容器：

```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" randomanswers
172.31.194.61
```

可以使用 IPv4 地址和配置的端口 (8000)（所示的示例中为 `http://172.31.194.61:8000`）连接到正在运行的容器。 在浏览器中键入该 URL，应该可看到正在运行的站点。

> [!NOTE]
> 某 VPN 或代理软件可能会阻止你导航到站点。
> 可以暂时禁用它，确保容器正常工作。

GitHub 上的示例目录包含为你执行这些命令的 [PowerShell 脚本](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator/run.ps1)。 打开 PowerShell 窗口，将目录更改为解决方案目录，然后键入：

```
./run.ps1
```

这将生成映像、在计算机上显示映像列表、启动容器，并显示该容器的 IP 地址。 

完成后，若要停止容器，可发出 `docker
stop` 命令：

```
docker stop randomanswers
```

若要删除该容器，可发出 `docker rm` 命令：

```
docker rm randomanswers
```

## <a name="summary"></a>摘要

在本主题中，已了解在 Windows Server 容器中移动和运行现有 ASP.NET MVC 应用程序的步骤。 运行现有应用程序不需要对其进行任何更改。 需要运行任务才能发布应用程序、生成 Docker 映像以及在新容器中启动映像。 利用 Windows Server 容器是将现有应用程序迁移到此环境的最简单途径。

[windows-container]: media/aspnetmvc/SwitchContainer.png "切换到 Windows 容器"
[publish-connection]: media/aspnetmvc/PublishConnection.png "发布到文件系统"
[publish-settings]: media/aspnetmvc/PublishSettings.png "发布设置"



<!--HONumber=Nov16_HO1-->


