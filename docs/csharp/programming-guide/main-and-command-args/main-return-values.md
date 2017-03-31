---
title: "Main() 返回值（C# 编程指南）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- Main method [C#], return values
ms.assetid: c2f5a1d8-1676-4bea-bc7e-44a97e72d5bc
caps.latest.revision: 20
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 846c52b7d5429a23f354dd6a732ddb62563a55bf
ms.lasthandoff: 03/13/2017

---
# <a name="main-return-values-c-programming-guide"></a>Main() 返回值（C# 编程指南）
`Main` 方法可以返回 `void`：  
  
 [!code-cs[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-return-values_1.cs)]  
  
 还可以返回 `int`：  
  
 [!code-cs[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-return-values_2.cs)]  
  
 如果未使用 `Main` 的返回值，则返回 `void` 可以使代码变得略微简单。 但是，返回整数可使程序将状态信息传递给调用可执行文件的其他程序或脚本。 以下示例演示了如何访问 `Main` 的返回值。  
  
## <a name="example"></a>示例  
 在本示例中，批文件用于运行程序并测试 `Main` 函数的返回值。 在 Windows 中执行程序时，从 `Main` 函数返回的任何值都存储在名为 `ERRORLEVEL` 的环境变量中。 批处理文件可以通过检查 `ERRORLEVEL` 变量来确定执行结果。 通常，返回值为零表示执行成功。 下例是从 `Main` 函数返回零的简单程序。 零表示程序已成功运行。 将该程序保存为 MainReturnValTest.cs。  
  
 [!code-cs[csProgGuideMain#14](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-return-values_3.cs)]  
  
## <a name="example"></a>示例  
 此示例使用了批处理文件，因此最好在命令提示中编译这段代码。 请按照[如何：为 Visual Studio 命令行设置环境变量](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)中的说明启用命令行生成，或使用 Visual Studio 命令提示符（可通过“开始”****菜单中的 **Visual Studio Tools** 访问）启用命令行生成。 从命令提示符，导航到保存程序的文件夹。 以下命令编译 MainReturnValTest.cs 并生成可执行文件 MainReturnValTest.exe。  
  
 `csc MainReturnValTest.cs`  
  
 接下来，创建一个批处理文件，运行 MainReturnValTest.exe 并显示结果。 将以下代码粘贴到文本文件中，并在包含 MainReturnValTest.cs 和 MainReturnValTest.exe 的文件夹中将其另存为 `test.bat`。 在命令提示符处键入 `test`运行该批处理文件。  
  
 因为代码返回零，所以批处理文件将报告成功。 但是，如果将 MainReturnValTest.cs 更改为返回非零值，然后重新编译程序，则批处理文件的后续执行将报告失败。  
  
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
  
## <a name="sample-output"></a>示例输出  
 `Execution succeeded`  
  
 `Return value = 0`  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 参考](../../../csharp/language-reference/index.md)   
 [Main() 和命令行自变量](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [如何：显示命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [如何：使用 foreach 访问命令行参数](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)
