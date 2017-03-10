---
title: "命令行参数（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "命令行参数 [C#]"
ms.assetid: 0e597e0d-ea7a-41ba-a38a-0198122f3c26
caps.latest.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 27
---
# 命令行参数（C# 编程指南）
通过以下方式之一定义方法，可以将参数发送至 `Main` 方法。  
  
 [!code-cs[csProgGuideMain#2](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/command-line-arguments_1.cs)]  
  
 [!code-cs[csProgGuideMain#3](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/command-line-arguments_2.cs)]  
  
> [!NOTE]
>  若要在 Windows 窗体应用程序中的 `Main` 方法中启用命令行参数，必须手动修改 program.cs 中 `Main` 的签名。  Windows 窗体设计器生成的代码创建没有输入参数的 `Main`。  也可以使用 <xref:System.Environment.CommandLine%2A?displayProperty=fullName> 或 <xref:System.Environment.GetCommandLineArgs%2A?displayProperty=fullName> 从控制台或 Windows 应用程序中的任何位置访问命令行参数。  
  
 `Main` 方法的参数是表示命令行参数的 <xref:System.String> 数组。  一般是通过测试 `Length` 属性来确定参数是否存在，例如：  
  
 [!code-cs[csProgGuideMain#4](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/command-line-arguments_3.cs)]  
  
 还可以使用 <xref:System.Convert> 类或 `Parse` 方法将字符串参数转换为数值类型。  例如，下面的语句使用 <xref:System.Int64.Parse%2A> 方法将 `string` 转换为 `long` 数字：  
  
```  
long num = Int64.Parse(args[0]);  
```  
  
 也可以使用别名为 `Int64` 的 C\# 类型 `long`：  
  
```  
long num = long.Parse(args[0]);  
```  
  
 还可以使用 `Convert` 类的方法 `ToInt64` 完成同样的工作：  
  
```  
long num = Convert.ToInt64(s);  
```  
  
 有关更多信息，请参见<xref:System.Int64.Parse%2A>和<xref:System.Convert>。  
  
## 示例  
 下面的示例演示如何在控制台应用程序中使用命令行参数。  应用程序在运行时采用一个参数，将该参数转换为整数，并计算该数的阶乘。  如果没有提供参数，则应用程序发出一条消息来解释程序的正确用法。  
  
 若要根据命令提示编译并运行应用程序，请执行以下步骤：  
  
1.  将以下代码粘贴到任何文本编辑器中，并将文件保存为名为 `Factorial.cs` 的文本文件。  
  
     [!code-cs[csProgGuideMain#16](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/command-line-arguments_4.cs)]  
  
2.  从“开始”屏幕或“开始”菜单中，打开 Visual Studio“开发人员命令提示”窗口，然后导航到包含您刚创建的文件的文件夹。  
  
3.  若要编译应用程序，请输入下面的命令。  
  
     `csc Factorial.cs`  
  
     如果您的应用程序中有没有编译错误，则将创建名为 `Factorial.exe` 的可执行文件。  
  
4.  输入以下命令来计算 3 的阶乘：  
  
     `Factorial 3`  
  
5.  此命令将生成以下输出：`The factorial of 3 is 6.`  
  
> [!NOTE]
>  在 Visual Studio 中运行应用程序时，可以在[“项目设计器”\-\>“调试”页](/visual-studio/ide/reference/debug-page-project-designer)中指定命令行参数。  
  
 有关如何使用命令行参数的更多示例，请参见[如何：使用命令行创建和使用程序集](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 请参阅  
 <xref:System.Environment?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [Main\(\) 和命令行参数](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [如何：显示命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [如何：使用 foreach 访问命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Main\(\) 返回值](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)   
 [类](../../../csharp/programming-guide/classes-and-structs/classes.md)