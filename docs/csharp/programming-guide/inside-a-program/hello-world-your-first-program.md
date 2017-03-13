---
title: "Hello World -- 您的第一个程序（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "get-started-article"
f1_keywords: 
  - "cs.program"
  - "vs.csharp.startpage.firstapplication"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "示例 [C#], Hello World"
  - "Hello World 示例 [C#]"
ms.assetid: 6493182a-b0b6-4539-a719-518a168cb730
caps.latest.revision: 39
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 39
---
# Hello World -- 您的第一个程序（C# 编程指南）
以下过程创建 C\# 版本的传统“Hello World\!”程序。  该程序显示字符串 `Hello World!`  
  
 有关入门概念的更多示例，请参见 [Visual C\# 和 Visual Basic 入门](/visual-studio/ide/getting-started-with-visual-csharp-and-visual-basic)。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 创建并运行控制台应用程序  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，选择**“文件”**，**“新建**、**“项目”**。  
  
     将打开**“新建项目”**对话框。  
  
3.  展开“已安装”，展开“模板”，展开“Visual C\#”，然后选择“控制台应用程序”。  
  
4.  在“名称”框中，指定项目名称，然后选中“确定”按钮。  
  
     新项目出现在**“解决方案资源管理器”**中。  
  
5.  如果 Program.cs 不是在“代码编辑器”中打开，则打开“解决方案资源管理器”中“Program.cs”的快捷方式菜单，然后选择“视图代码”。  
  
6.  用下面的代码替换 Program.cs 的内容。  
  
     [!code-cs[csProgGuide#21](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_1.cs)]  
  
7.  选择 F5 键运行项目。  命令提示窗口将显示，其中包含行 `Hello World!`  
  
 接着，检查本程序的重要部分。  
  
## 注释  
 第一行包含注释。  `//` 字符将这行的其余内容转换为注释内容。  
  
 [!code-cs[csProgGuide#32](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_2.cs)]  
  
 还可通过将文本块置于 `/*` 和 `*/` 字符之间将其注释掉。  这将在下面的示例中显示。  
  
 [!code-cs[csProgGuide#33](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_3.cs)]  
  
## Main 方法  
 C\# 控制台应用程序必须包含一个 `Main` 方法，用于控制程序的开始和结束。  在 `Main` 方法中创建对象和执行其他方法。  
  
 `Main` 方法是驻留在类或结构内的 [static](../../../csharp/language-reference/keywords/static.md)方法。  在前面的“Hello World\!”示例中，此方法驻留在一个名为 `Hello` 的类中。  可以用下列方式之一声明 `Main` 方法：  
  
-   该方式返回 `void`。  
  
     [!code-cs[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_4.cs)]  
  
-   它还可以返回整数。  
  
     [!code-cs[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_5.cs)]  
  
-   由于有任意一个返回类型，它可以带有参数。  
  
     [!code-cs[csProgGuideMain#19](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_6.cs)]  
  
     \- 或 \-  
  
     [!code-cs[csProgGuideMain#18](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_7.cs)]  
  
 `Main` 方法的参数是 `args` 和 `string` 数组，该数组包含用于激活程序的命令行参数。  与 C\+\+ 不同，数组不包含可执行 \(exe\) 文件的文件名。  
  
 有关如何使用命令行参数的更多信息，请参见 [Main\(\) 和命令行参数](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)中的示例和[如何：使用命令行创建和使用程序集](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 通过按 F5 在调试模式下运行程序时，在 `Main` 方法的末尾调用 <xref:System.Console.ReadKey%2A> 将使得控制台窗口无法关闭，从而使您无法阅读输出。  
  
## 输入和输出  
 C\# 程序通常使用 .NET Framework 的运行库提供的输入\/输出服务。  `System.Console.WriteLine("Hello World!");` 语句使用 <xref:System.Console.WriteLine%2A> 方法。  此方法是运行库中的 <xref:System.Console> 类的输出方法之一。  它显示了标准输出流使用的字符串参数，输出流后面跟一个新行。  其他 <xref:System.Console> 方法用于不同的输入和输出操作。  如果程序开始处包含 `using System;` 指令，则无需完全限定 <xref:System> 类和方法即可直接使用它们。  例如，您可以改为调用 `Console.WriteLine` 而非 `System.Console.WriteLine`：  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_8.cs)]  
  
 [!code-cs[csProgGuide#23](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_9.cs)]  
  
 有关输入\/输出方法的更多信息，请参见 <xref:System.IO>。  
  
## 命令行编译和执行  
 可以使用命令行而不是 Visual Studio 集成开发环境 \(IDE\) 编译“Hello World\!”程序。  
  
#### 从命令提示行编译并运行  
  
1.  将前面过程的代码粘贴到任何文本编辑器中，并将文件保存为文本文件。  文件 `Hello.cs` 的名称。  C\# 源代码文件使用的扩展名是 `.cs`。  
  
2.  执行以下步骤之一打开命令提示符窗口：  
  
    -   在 Windows 8 中，在“开始”屏幕，搜索`开发人员命令提示`，然后点击或选择“VS2012 开发人员命令提示”。  
  
         将出现“开发人员命令提示符”窗口。  
  
    -   在 Windows 7 中，打开“开始”菜单，展开当前 Visual Studio 版本的文件夹，打开“Visual Studio 工具”的快捷菜单，然后选择“VS2012 开发人员命令提示”。  
  
         将出现“开发人员命令提示符”窗口。  
  
    -   从标准“命令提示”窗口启用命令行生成。  
  
         请参见 [How to: Set Environment Variables for the Visual Studio Command Line](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)。  
  
3.  在命令提示窗口中，导航至包含 `Hello.cs` 文件的文件夹。  
  
4.  输入下面的命令，编译 `Hello.cs`。  
  
     `csc Hello.cs`  
  
     如果您的程序中有没有编译错误，则将创建名为 `Hello.exe` 的可执行文件。  
  
5.  命令提示符窗口中，输入以下命令运行程序：  
  
     `Hello`  
  
 有关 C\# 编译器及其选项的详细信息，请参阅 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)。  
  
## 重要章节  
 在 [Visual C\# 2010 使用入门](http://go.microsoft.com/fwlink/?LinkId=221214)中[编写 C\# 程序](http://go.microsoft.com/fwlink/?LinkId=221227)  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [在 C\# 程序内部](../../../csharp/programming-guide/inside-a-program/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [\<paveover\>C\# Sample Applications](http://msdn.microsoft.com/zh-cn/9a9d7aaa-51d3-4224-b564-95409b0f3e15)   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [Main\(\) 和命令行参数](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [Visual C\# 和 Visual Basic 入门](/visual-studio/ide/getting-started-with-visual-csharp-and-visual-basic)