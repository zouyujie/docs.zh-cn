---
title: "使用 Visual Studio 2017 发布 Hello World 应用程序"
description: "使用 Visual Studio 2017 发布 Hello World 应用程序"
keywords: ".NET, .NET Core, .NET Core 控制台应用程序, 发布 (.NET Core), 部署 (.NET Core)"
author: BillWagner
ms.author: wiwagn
ms.date: 10/24/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a19545d3-24af-4a32-9778-cfb5ae938287
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f4a30d19e111d395088e38c4543c9dacee6105fd
ms.lasthandoff: 03/13/2017

---

# <a name="publishing-your-hello-world-application-with-visual-studio-2017"></a>使用 Visual Studio 2017 发布 Hello World 应用程序

你在[使用 Visual Studio 2017 生成 C# .NET Core Hello World 应用程序](with-visual-studio-2017.md)中生成了 Hello World 控制台应用程序，然后在[使用 Visual Studio 2017 调试 C# Hello World 应用程序](debugging-with-visual-studio-2017.md)中使用 Visual Studio 调试器对其进行了测试。 至此，你已确定应用程序能够按预期运行，可以发布它以供其他用户运行了。 发布应用程序会创建运行应用程序所需的一组文件；可以通过将这些文件复制到目标计算机来进行部署。

若要发布并运行应用程序，请执行以下操作： 

1. 请确保 Visual Studio 生成的是应用程序的发行版本。 必要时，将工具栏上的生成配置设置从“调试”****更改为“发行”****，如下图所示。

   ![Image](media/release.jpg)

1. 打开控制台窗口。 例如，在 Windows 任务栏的“有问题尽管问我”****文本框中，输入“`Command Prompt`”，然后选择“命令提示符”****桌面应用程序，打开控制台窗口。

1. 右键单击 HelloWorld 项目（而不是 HelloWorld 解决方案），然后选择菜单中的“发布”****。 还可以选择“生成”****Visual Studio 主菜单中的“发布 HelloWorld”****。

1. 看到下图所示的“发布”****对话框时，选择“创建新配置文件”****，新建发布配置文件。

1. 在下图所示的“选取发布目标”****对话框中，选择“确定”****按钮，将应用程序发布到本地文件系统。 程序将位于应用程序项目目录的 bin\release\PublishOutput 子目录中。

1. 至此，你已创建发布配置文件，请选择“发布”****对话框中的“发布”****按钮，如下图所示。

   ![Image](media/publish-2.jpg)

1. 如下图所示，已发布的输出包括以下三个组成应用程序的文件，可以通过将这些文件复制到目标系统进行部署：

      - HelloWorld.dll
   
      - HelloWorld.deps.json

      - HelloWorld.runtimeconfig.json

   第四个文件 HelloWorld.pdb 包含调试符号。 无需将此文件与应用程序一起分发，尽管应在需要调试应用程序的发布版本的情况下保存此文件。

   ![Image](media/pub-files.jpg)

发布过程会生成依赖于框架的部署；发布的应用程序将在 .NET Core 支持的任何平台上运行，只要系统上安装了 .NET Core 即可。 用户可以通过在控制台窗口中发出 `dotnet.exe HelloWorld.dll` 命令来运行应用程序。

若要详细了解如何发布和部署 .NET Core 应用程序，请参阅 [.NET Core 应用程序部署](../../core/deploying/index.md)。
