---
title: "将 MSTest 与 Windows 上的 .NET Core 配合使用"
description: "如何通过 Visual Studio 2015 将 MSTest 与 Windows 上的 .NET Core 配合使用"
keywords: MSTest, .NET, .NET Core
author: ncarandini
ms.author: wiwagn
ms.date: 08/18/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ed447641-3e85-4e50-b7ed-004630048a3e
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 94304cd742b63e77126bfa40651faa6974e58853
ms.lasthandoff: 03/03/2017

---

# <a name="unit-testing-with-mstest-and-net-core-on-windows-using-visual-studio-2015"></a>通过 Visual Studio 2015 将 MSTest 与 Windows 上的 .NET Core 配合使用的单元测试

尽管面向多个平台时 xUnit 是更好的选择，借助 Windows 上的 .NET Core 同样可以使用 MSTest。

## <a name="prerequisites"></a>先决条件

按照 [Windows 上的 .NET Core 入门](../tutorials/using-on-windows.md)中的说明创建库项目。

### <a name="writing-the-test-project-using-mstest"></a>使用 MSTest 编写测试项目

1. 在“解决方案资源管理器”中，打开“解决方案”节点的上下文菜单，然后选择“添加”、“新解决方案文件夹”。 将文件夹命名为“test”。 
   这只是解决方案文件夹，不是物理文件夹。

2. 打开 **test** 文件夹的上下文菜单，选择“添加”。 “新建项目”。 在“新建项目”对话框中，选择“控制台应用程序 (.NET Core)”。 将其命名为“TestLibrary”，并显式放置到 `Golden\test` 路径下。 

   > [!IMPORTANT]
   > 该项目必须是控制台应用程序，不能是类库。

3. 在“TestLibrary”项目中，打开“引用”节点的上下文菜单，选择“添加引用”。 

4. 在“引用管理器”对话框中，选中“项目”、“解决方案”节点下的“库”，然后单击“确定”。 

5. 在“TestLibrary”项目中，打开 `project.json` 文件，将 `"Library": "1.0.0-*"` 替换为 `"Library": {"target": "project"}`。 

   这是为了避免将 `Library` 项目解析到具有相同名称的 NuGet 包。 将目标显式设置为“项目”可确保工具首先搜索具有此名称的项目，而不是包。 

6. 打开“引用”节点的上下文菜单，并选择“管理 NuGet 包”。

7. 选择“nuget.org”作为“包源”，并选择“浏览”选项卡。 选中“包括预发行版”复选框，然后浏览 **MSTest.TestFramework** 1.0.1 预览版或更新版本，然后单击“安装”。 

8. 浏览 **dotnet-test-mstest** 1.1.1 预览版或更新版本，然后单击“安装”。

9. 编辑 `project.json` 以在 `"version"` 部分后添加 `"testRunner": "mstest",`。

10. 将 `LibraryTests.cs` 类文件添加到 **TestLibrary** 项目，将 `using` 指令 `Microsoft.VisualStudio.TestTools.UnitTesting;` 和 `using Library;` 添加到文件顶部并将以下代码添加到类：
    ```csharp
    [TestClass]
    public class LibraryTests
    {
        [TestMethod]
        public void ThingGetsObjectValFromNumber()
        {
            Assert.AreEqual(42, new Thing().Get(42));
        }
    }
    ```
    * 或者，从 **TestLibrary** 项目删除 `Program.cs` 文件，并从 `project.json` 删除 `"buildOptions": {"emitEntryPoint": true},`。

   现在，应该可以生成解决方案了。 
   
11. 在“测试”菜单上，选择“Windows”、“测试资源管理器”，在测试资源管理器中选择“全部运行”。
   
   测试应该会通过。

