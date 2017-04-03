---
title: "使用 Visual Studio 2017 生成 C# .NET Core Hello World 应用程序"
description: "了解如何使用 Visual Studio 2017 生成简单的 .NET Core 控制台应用程序。"
keywords: ".NET Core, .NET Core 控制台应用程序, Visual Studio 2017"
author: stevehoag
ms.author: shoag
ms.date: 03/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 97aa50bf-bdf8-416d-a56c-ac77504c14ea
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f1a20f399b4ab34986d700622ff3bf3859b001bd
ms.lasthandoff: 03/13/2017

---

# <a name="building-a-c-hello-world-application-with-net-core-in-visual-studio-2017"></a>使用 Visual Studio 2017 生成 C# .NET Core Hello World 应用程序 #

本主题介绍了有关使用 Visual Studio 2017 生成、调试和发布简单的 .NET Core 控制台应用程序的分步说明。 Visual Studio 2017 提供了功能全面的开发环境，可用于生成 .NET Core 应用程序。 只要应用程序没有任何平台专属依赖项，应用程序本身就可以在 .NET Core 定位的任何平台上和安装了 .NET Core 的任何系统上运行。

## <a name="prerequisites"></a>先决条件 ##

- 安装了“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://www.visualstudio.com/downloads/)。 

有关详细信息，请参阅“Windows 系统必备”主题中的 [Visual Studio 2017](../../core/windows-prerequisites.md) 部分。

## <a name="a-simple-hello-world-application"></a>简单的“Hello World”应用程序 ##

首先，我们要创建简单的“Hello World”控制台应用程序。 步骤如下：

1. 启动 Visual Studio，然后依次选择“文件”****菜单上的“新建”**** > “项目”****。 在“新建项目”****对话框中，展开左侧窗格中的“Visual C#”****节点，然后选择“.NET Core”****节点。

2. 在右侧窗格中，选择“控制台应用程序 (.NET Core)”****。 输入项目名称 `HelloWorld`，并务必选中“创建解决方案的目录”****框，如下图所示。

   ![显示在“新建项目”对话框中选择了“控制台应用程序”的屏幕截图](./media/with-visual-studio/vs_newproject.jpg)
   
3. 选择“确定” **** 按钮。 此时，Visual Studio 会显示带代码窗口的开发环境，如下图所示。 C# .NET Core 控制台应用程序模板会自动定义类 `Program` 和一个需要将 @System.String 数组用作自变量的方法 `Main`。 `Main` 是应用程序入口点，同时也是在应用程序启动时由运行时自动调用的方法。 *args* 数组中包含在应用程序启动时提供的所有命令行自变量。

   ![Visual Studio 和新建的 HelloWorld 项目](./media/with-visual-studio/vs_devenv.jpg)

   此模板创建的是非常简单的“Hello World”应用程序，可调用 @System.Console.WriteLine(System.String) 方法在控制台窗口中显示文本字符串“Hello World!” 。 现在，选择工具栏上含绿色箭头的“HelloWorld”按钮，可以在调试模式下运行程序。 不过，如果这样做，控制台窗口的可见时间很短，然后就关闭了。 这是因为在 `Main` 方法中的一个语句执行后，`Main` 和应用程序立即终止。

4. 我们要让现有的应用程序在关闭控制台窗口前先暂停一下。 在 @System.Console.WriteLine(System.String) 方法调用后面紧接着添加以下代码：

   ```csharp
   Console.Write("Press any key to continue...");
   Console.ReadKey(true);
   ```
   此代码会提示用户按任意键，然后在用户按键前暂停程序。

5. 在菜单栏上，依次选择 **“生成”**、 **“生成解决方案”**。 这会将程序编译成 IL，这是一种中间语言，然后可由实时 (JIT) 编译器转换成二进制代码。

6. 选择工具栏上含绿色箭头的“HelloWorld”按钮，从而运行程序。 结果如下图所示。

   ![Image](./media/with-visual-studio/simple_hello.jpg)

7. 按任意键关闭窗口。

## <a name="enhancing-the-hello-world-application"></a>改进“Hello World”应用程序 ##

让我们来改进一下应用程序，使其提示用户输入他/她的姓名，然后在控制台窗口中显示用户姓名以及日期和时间。 若要修改和测试程序，请执行以下操作：

1. 在代码窗口中，在 `public static void Main(string[] args)` 代码行后面的左大括号和第一个右大括号之间，输入以下 C# 代码。

   [!CODE [GettingStarted#1](../../../samples/snippets/csharp/getting_started/with_visual_studio/helloworld.cs#1)]

   下图展示了生成的代码窗口。

   ![修改后的程序正在运行](./media/with-visual-studio/codewindow.jpg)

   此代码在控制台中显示“What is your name?”， 然后等待用户输入字符串并按 Enter 键。 它将此字符串存储到 `name` 变量中。 它还会检索 @System.DateTime.Now 属性的值（其中包含当前的本地时间），并将此值赋给 `date` 变量。 然后，它使用[复合格式字符串](../../standard/base-types/composite-format.md)在控制台中显示这些值。

2. 依次选择“生成”**** > “生成解决方案”****，编译此程序。 这会将程序编译成 IL，这是一种中间语言，然后可由实时 (JIT) 编译器转换成二进制代码。

3. 选择工具栏上的绿色箭头、按 F5 或依次选择“调试”**** > 和“启动调试”****菜单项，在调试模式下运行程序。 通过根据提示输入姓名并按 Enter 键后，控制台窗口应如下所示：

   ![修改后的程序正在运行](./media/with-visual-studio/console.jpg)

4. 按任意键关闭控制台窗口。 这将结束调试模式。

至此，你已创建并运行简单的应用程序。 若要开发专业应用程序，仍需要执行其他一些步骤，才能让应用程序可供发布：

- 若要了解如何调试应用程序，请参阅[调试 Hello World 应用程序](debugging-with-visual-studio-2017.md)

- 若要了解如何开发和发布可分发版本的应用程序，请参阅[发布 Hello World 应用程序](publishing-with-visual-studio-2017.md)。

## <a name="related-topics"></a>相关主题 ##

还可以使用 Visual Studio 2017 生成 .NET Core 类库，而不是控制台应用程序。 有关分步说明，请参阅[使用 Visual Studio 2017 生成 C# .NET Core 类库](library-with-visual-studio-2017.md)。

还可以使用 Visual Studio Code（可免费下载的代码编辑器）开发在 Mac、Linux 和 Windows 上运行的 .NET Core 控制台应用程序。 有关分步教程，请参阅 [Visual Studio Code 入门](with-visual-studio-code.md)。

