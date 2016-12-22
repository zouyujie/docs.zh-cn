---
title: "#line（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "#line"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#line 指令 [C#]"
ms.assetid: 6439e525-5dd5-4acb-b8ea-efabb32ff95b
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #line（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`#line` 使您可以修改编译器的行号以及（可选）错误和警告的文件名输出。  下面的示例说明如何报告与行号关联的两个警告。  `#line 200` 指令将行号强制设置为 200（尽管默认行号为 \#7），在执行下一条 \#line 指令之前，文件名将报告为“Special”。  \#line default 指令将行号恢复为默认行号，默认行号对前一条指令重新编号的行进行计数。  
  
```  
class MainClass  
{  
    static void Main()  
    {  
#line 200 "Special"  
        int i;    // CS0168 on line 200  
        int j;    // CS0168 on line 201  
#line default  
        char c;   // CS0168 on line 9  
        float f;  // CS0168 on line 10  
#line hidden // numbering not affected  
        string s;   
        double d; // CS0168 on line 13  
    }  
}  
```  
  
## 备注  
 `#line` 指令可能由生成过程中的自动中间步骤使用。  例如，如果行从原始的源代码文件中移除，但是您仍希望编译器基于文件中的原始行号生成输出，则可以移除行，然后用 `#line` 模拟原始行号。  
  
 `#line hidden` 指令对调试器隐藏若干连续的行，这样当开发人员在逐句通过代码时，将会跳过 `#line hidden` 和下一个 `#line` 指令（假定它不是另一个 `#line hidden` 指令）之间的所有行。  此选项也可用来使 ASP.NET 能够区分用户定义的代码和计算机生成的代码。  尽管 ASP.NET 是此功能的主要使用者，但很可能将有更多的源生成器使用它。  
  
 `#line hidden` 指令不会影响错误报告中的文件名或行号。  即，如果在隐藏块中遇到错误，编译器将报告当前文件名和错误的行号。  
  
 `#line filename` 指令指定您希望出现在编译器输出中的文件名。  默认情况下，使用源代码文件的实际名称。  文件名必须用双引号 \(""\) 引起来且前面必须带一个行号。  
  
 源代码文件可以具有 `#line` 指令的任何编号。  
  
## 示例 1  
 下面的示例说明调试器如何忽略代码中的隐藏行。  运行此示例时，它将显示三行文本。  但是，当设置如示例所示的断点并按 F10 键逐句通过代码时，您将看到调试器忽略了隐藏行。  还请注意，即使在隐藏行上设置断点，调试器仍会忽略它。  
  
```  
// preprocessor_linehidden.cs  
using System;  
class MainClass   
{  
    static void Main()   
    {  
        Console.WriteLine("Normal line #1."); // Set break point here.  
#line hidden  
        Console.WriteLine("Hidden line.");  
#line default  
        Console.WriteLine("Normal line #2.");  
    }  
}  
```  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)