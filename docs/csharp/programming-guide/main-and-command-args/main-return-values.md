---
title: "Main() 返回值（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Main 方法 [C#], 返回值"
ms.assetid: c2f5a1d8-1676-4bea-bc7e-44a97e72d5bc
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Main() 返回值（C# 编程指南）
`Main` 方法可以返回 `void`：  
  
 [!code-cs[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/main-return-values_1.cs)]  
  
 它还可以返回 `int`：  
  
 [!code-cs[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/main-return-values_2.cs)]  
  
 如果不使用 `Main` 的返回值，则返回 `void` 可以稍微简化代码。  但是，如果返回整数，则程序可以与调用该可执行文件的其他程序或脚本交流状态信息。  下面的示例演示如何访问 `Main` 的返回值。  
  
## 示例  
 此示例使用一个批处理文件来运行程序，并测试 `Main` 函数的返回值。  在 Windows 中执行程序时，`Main` 函数返回的任何值都将存储在名为 `ERRORLEVEL` 的环境变量中。  通过检查 `ERRORLEVEL` 变量，批处理文件可以确定执行结果。  通常，返回值为零指示执行成功。  下面是一个简单程序示例，从 `Main` 函数返回零。  零指示程序成功运行。  请将该程序保存为 MainReturnValTest.cs。  
  
 [!code-cs[csProgGuideMain#14](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/main-return-values_3.cs)]  
  
## 示例  
 此示例使用了批处理文件，因此最好在命令提示中编译这段代码。  请按照[How to: Set Environment Variables for the Visual Studio Command Line](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)中的说明启用命令行生成，或者使用 Visual Studio 命令提示（可通过**“开始”**菜单中的**“Visual Studio Tools”**访问）。  在命令提示符下，定位到保存程序的文件夹。  下面的命令编译 MainReturnValTest.cs，生成可执行文件 MainReturnValTest.exe。  
  
 `csc MainReturnValTest.cs`  
  
 接下来，创建一个批处理文件，运行 MainReturnValTest.exe 并显示结果。  将下面的代码粘贴到文本文件中，将该文件另存为 `test.bat`，保存到包含 MainReturnValTest.cs 和 MainReturnValTest.exe 的文件夹中。  在命令提示符下，键入 `test`，运行该批处理文件。  
  
 因为代码返回零，所以该批处理文件会报告成功。  但是，如果将 MainReturnValTest.cs 更改为返回非零值，然后重新编译程序，则批处理文件的后续执行将报告失败。  
  
```  
rem test.bat  
@echo off  
MainReturnValTest  
@if "%ERRORLEVEL%" == "0" goto good  
  
:fail  
    echo Execution Failed  
    echo return value = %ERRORLEVEL%  
    goto end  
  
:good  
    echo Execution succeeded  
    echo Return value = %ERRORLEVEL%  
    goto end  
  
:end  
```  
  
## 示例输出  
 `Execution succeeded`  
  
 `Return value = 0`  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [Main\(\) 和命令行参数](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [如何：显示命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [如何：使用 foreach 访问命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)