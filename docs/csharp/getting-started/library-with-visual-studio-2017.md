---
title: "使用 Visual Studio 2017 生成 C# .NET Core 类库"
description: "了解如何使用 Visual Studio 2017 生成用 C# 编写的类库"
keywords: ".NET Core, .NET 标准类库, Visual Studio 2017"
author: stevehoag
ms.author: shoag
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: c849ca26-6a25-4d35-9544-f343af88e0e7
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 28fa60cdcf8e0056314af271208759eadd8503a5
ms.lasthandoff: 03/13/2017

---

# <a name="building-a-class-library-with-c-and-net-core-in-visual-studio-2017"></a>使用 Visual Studio 2017 生成 C# .NET Core 类库 #

类库定义的是可以从任意应用程序调用的类型和方法。 使用 .NET Core 开发的类库支持 .NET 标准库，这样任何支持相应版本 .NET 标准库的 .NET 平台都可以调用你的库。 完成类库时，可以决定是要将其作为第三方组件进行分发，还是要将其作为与一个或多个应用程序捆绑在一起的组件进行添加。

> [!NOTE]
> 有关 .NET 标准版及其支持的平台列表，请参阅 [.NET 标准库](../../standard/library.md)。

在本主题中，我们将创建包含一个字符串处理方法的简单实用工具库。 我们将把它作为[扩展方法](../../csharp/programming-guide/classes-and-structs/extension-methods.md)进行实现，这样就可以把它作为 @System.String 类成员进行调用。

## <a name="creating-a-class-library-solution"></a>创建类库解决方案 ##

首先，我们要为类库项目及其相关项目创建解决方案。 Visual Studio 解决方案只用作一个或多个项目的容器。 若要创建解决方案，请执行以下操作：

1. 在 Visual Studio 菜单栏上，依次选择“文件”****、“新建”****和“项目”****。

1. 在“新建项目”****对话框中，展开“其他项目类型”****节点，然后选择“Visual Studio 解决方案”****，如下图所示。

   ![Image](./media/solution.jpg)

1. 将解决方案命名为“ClassLibraryProjects”，然后选择“确定”****按钮。 下图显示结果。

   ![Image](./media/vs_with_solution.jpg)

## <a name="creating-the-class-library-project"></a>创建类库项目 ##

现在，可以创建我们的类库项目：

1. 在“解决方案资源管理器”****中，打开“ClassLibraryProjects”****节点的上下文菜单，然后依次选择“添加”****和“新项目”****。

1. 在“添加新项目”****对话框中，依次选择“.NET Core”****节点和“类库(.NET 标准)”****项目模板。

1. 在“名称”****文本框中，输入项目名称“StringLibrary”，如下图所示。

   ![Image](./media/lib_project.jpg)

1. 选择“确定”****，创建类库项目。 下图显示结果。

   ![Image](./media/class_library.jpg)

1. 将代码窗口中的代码替换为以下代码：

   [!CODE-csharp[ClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/classlib.cs#1)]

   类库 `UtilityLibraries.StringLibrary` 包含 `StartsWithUpper` 方法，此方法会返回 @System.Boolean 值，以指明当前字符串实例是否以大写字符开头。 具体哪些是大写字符由 Unicode 标准定义。 在 .NET Core 中，如果字符为大写，则 [Char.IsUpper](xref:System.Char.IsUpper(System.Char)) 方法返回 `true`。

1. 在菜单栏上，依次选择 **“生成”**、 **“生成解决方案”**。 此项目的编译应该没有错误。

## <a name="the-next-step"></a>后续步骤 ##

至此，我们已成功生成类库。 不过，由于我们尚未调用库的任何方法，因此还不知道它能否按预期运行。 开发类库的下一步是使用 [C# 单元测试项目](testing-library-with-visual-studio.md)来测试它。



