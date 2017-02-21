---
title: "使用 Visual Studio 2017 在 Windows 上实现 .NET Core 入门 | Microsoft Docs"
description: "使用 Visual Studio 2017 在 Windows 上实现 .NET Core 入门"
keywords: ".NET、.NET Core"
author: bleroy
ms.author: mairaw
ms.date: 01/18/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 613c65d0-f773-41b8-ba0e-83f6a82a0b30
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: cc2c2853bc31e161d1fe0de4edc71d15281c6d24

---

# <a name="getting-started-with-net-core-on-windows-using-visual-studio-2017-net-core-tools-rc4"></a>使用 Visual Studio 2017 在 Windows 上开始使用 .NET Core（.NET Core 工具 RC4）

> [!WARNING]
> 本主题适用于 .NET Core 工具 RC4。 对于 Visual Studio 2015 - .NET Core 工具预览版 2，请参阅[使用 Visual Studio 2015 在 Windows 上入门 .NET Core](../../tutorials/using-on-windows.md) 主题。

Visual Studio 2017 提供用于开发 .NET Core 应用程序的功能全面的开发环境。 本文档中的过程描述了使用 Visual Studio 和 .NET Core 生成非常简单的控制台应用程序所需的步骤。

## <a name="prerequisites"></a>先决条件

请按照[先决条件页](../windows-prerequisites.md)上的说明更新环境。

## <a name="getting-started"></a>入门

以下步骤将为 .NET Core 控制台应用程序开发设置 Visual Studio 2017：

1. 打开 Visual Studio，在“文件”菜单上，选择“新建”、“项目”。

2. 在“新建项目”对话框的“模板”列表中，展开“Visual C#”节点并选择“.NET Core”。 应该可以看到“控制台应用 (.NET Core)”、“类库 (.NET Standard)”、“单元测试项目 (.NET Core)”、“类库 (.NET Core)”和“ASP.NET Core Web 应用程序 (.NET Core)”的五个项目模板。 选择“控制台应用 (.NET Core)”，键入项目的名称，选择位置，然后单击“确定”。

  ![新建项目：控制台应用](media/new-project-console-app.png)

3. 生成的项目有一个单独的 C# 文件，它会将“Hello World”输出到控制台。

  ![控制台应用项目](media/console-app-solution.png)

可以使用 F5 在调试模式下运行此应用程序，或使用 Ctrl + F5 在发布模式下运行此应用程序。 还可以设置断点以中断执行和检查变量，或开始编写更有趣的代码。

祝你编码愉快！

## <a name="next-steps"></a>后续步骤

经过以上简单介绍，你可能会想了解如何使用可重用的库和测试来生成更高级的解决方案。 [使用 Visual Studio 2017 在 Windows 上构建完整的 .NET Core 解决方案](using-on-windows-vs-2017-full-solution.md)主题将告诉你如何操作。



<!--HONumber=Feb17_HO2-->


