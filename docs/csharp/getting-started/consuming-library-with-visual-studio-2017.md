---
title: "使用 Visual Studio 2017 调用 .NET Core 类库"
description: "了解如何使用 Visual Studio 2017 调用类库中的成员"
keywords: ".NET Core, .NET Core 类库, .NET 标准, .NET 标准类库分发"
author: stevehoag
ms.author: shoag
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: d7b94076-1108-4174-94e7-a18f00072bb7
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0b42eeb0149feec09ddacba98383da3abd53bb5e
ms.lasthandoff: 03/13/2017

---

# <a name="consuming-a-class-library-with-net-core-in-visual-studio-2017"></a>使用 Visual Studio 2017 调用 .NET Core 类库 #

如果你已按照[使用 Visual Studio 2017 生成 C# .NET Core 类库](./library-with-visual-studio-2017.md)和[使用 Visual Studio 2017 测试 .NET Core 类库](testing-library-with-visual-studio.md)中的步骤操作生成和测试类库，并且已生成类库的发行版本，下一步就是使其可供调用方使用。 可以通过以下两种方式执行此操作：

- 如果类库将供一个解决方案使用（例如，如果它是一个大型应用程序中的组件），可以直接将其以项目的形式添加到解决方案中。

- 如果类库将供更多调用方使用，可以 NuGet 包的形式分发它。

## <a name="including-a-library-as-a-project-in-a-solution"></a>将类库以项目的形式添加到解决方案中 ##

就像我们将单元测试和类库添加到同一解决方案中一样，我们可以将应用程序添加到同一解决方案中。 例如，我们将在控制台应用程序中使用类库，此应用程序将提示用户输入字符串，并报告第一个字符是否为大写：

1. 打开在主题[使用 Visual Studio 2017 生成 C# .NET Core 类库](./library-with-visual-studio-2017.md)中创建的 `ClassLibraryProjects` 解决方案，然后在“解决方案资源管理器”中，打开 **ClassLibraryProjects** 节点的上下文菜单，然后依次选择“添加”****和“新项目”****。

1. 在“添加新项目”****对话框中，依次展开“Visual C#”****和“.NET Core”****节点，然后选择“控制台应用程序(.NET Core)”****项目模板，如下图所示。

   ![Image](./media/use-library.jpg)

1. 在“名称”****文本框中，输入“`ShowCase`”，然后选择“确定”****按钮。

1. 在“解决方案资源管理器”中，打开“ShowCase”****项目节点的上下文菜单，然后选择“设为启动项目”****。

1. 我们的项目一开始无权访问我们的类库。 若要允许我们的项目调用类库中的方法，请在“解决方案资源管理器”****中，打开“ShowCase”****项目中“依赖项”****节点的上下文菜单，然后选择“添加引用”****。

1. 在“引用管理器”****对话框中，选中我们的类库项目“StringLibrary”****（如下图所示），然后选择“确定”****按钮。

   ![Image](./media/add-lib-ref.jpg)

1. 在“program.cs”文件的代码窗口中，将所有代码替换为以下代码：

 [!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs#1)]

   此代码使用 [Console.WindowHeight](xref:System.Console.WindowHeight) 属性来确定控制台窗口中的行数。 只要 [Console.CursorTop](xref:System.Console.CursorTop) 属性大于或等于控制台窗口中的总行数，此代码就会清除控制台窗口，然后重新向用户显示消息。

   程序本身就是提示用户输入字符串。 然后指明字符串是否以大写字符开头。 如果用户没有输入字符串就按 **Enter** 键，那么控制台窗口会关闭，应用程序会终止。

1. 必要时，将工具栏更改为编译 `ShowCase` 项目的“调试”****版本，如下图所示。

   ![Image](./media/showcase-toolbar.jpg)

1. 单击“ShowCase”****按钮上的绿色箭头，编译并运行程序。

然后，可以按照[使用 Visual Studio 2017 调试 C# Hello World 应用程序](debugging-with-visual-studio-2017.md)和[使用 Visual Studio 2017 发布 Hello World 应用程序](publishing-with-visual-studio-2017.md)中列出的步骤操作，调试并最终发布使用此类库的应用程序。

## <a name="distributing-the-library-in-a-nuget-package"></a>以 NuGet 包的形式分发类库 ##

可以 NuGet 包的形式分发类库，让类库可供更多调用方使用。 Visual Studio 不支持创建 NuGet 包。 若要创建 NuGet 包，请使用 [`dotnet.exe` 命令行实用工具](../../core/tools/dotnet.md)，如下所示：

1. 打开控制台窗口。 例如，在 Windows 任务栏的“有问题尽管问我”****文本框中，输入“`Command Prompt`”，然后选择“命令提示符”****桌面应用程序，打开控制台窗口。

1. 转到类库的项目目录。 除非你重新配置了文件位置，否则通常位于 `Documents\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary` 目录中。 此目录包含源代码和项目文件 `StringLibrary.csproj`。

1. 发出命令 `dotnet.exe pack --no-build`。 此时，`dotnet.exe` 实用工具会生成一个扩展名为 .nupkg 的包。

   > [!TIP]
   > 如果路径中没有包含 `dotnet.exe` 的目录，可以通过在控制台窗口中输入“`where dotnet.exe`”来找到它的位置。

若要详细了解如何创建 NuGet 包，请参阅[如何使用跨平台工具创建 NuGet 包](../../core/deploying/creating-nuget-packages.md)。
