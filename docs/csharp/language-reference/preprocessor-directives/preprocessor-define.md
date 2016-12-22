---
title: "#define（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "#define"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#define 指令 [C#]"
ms.assetid: 23638b8f-779c-450e-b600-d55682de7d01
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #define（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用 `#define` 定义符号。  当您将符号用作传递给 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 指令的表达式时，此表达式的计算结果为 `true`，如下例所示：  
  
 `#`  `define`   `DEBUG`  
  
## 备注  
  
> [!NOTE]
>  不能像在 C 和 C\+\+ 中的通常做法一样，使用 `#define` 指令来声明常数值。  最好是将 C\# 中的常数定义为类或结构的静态成员。  如果具有多个像这样的常数，可以考虑创建一个单独的“Constants”类来保存这些常数。  
  
 符号可用于指定编译的条件。  可以使用 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 或 [\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md) 来测试符号。  还可以使用 `conditional` 特性执行条件编译。  
  
 可以定义符号，但是无法对符号赋值。  `#define` 指令必须在使用任何不是预处理器指令的指令之前出现在文件中。  
  
 也可以用 [\/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md) 编译器选项来定义符号。  可以用 [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md) 来取消定义符号。  
  
 用 `/define` 或 `#define` 定义的符号与具有同一名称的变量不冲突。  即，不应将变量名传递到预处理器指令，并且只能用预处理器指令计算符号。  
  
 用 `#define` 创建的符号范围是在其中定义该符号的文件。  
  
 如以下示例所示，您必须将 `#define` 指令置于文件的顶部。  
  
```c#  
#define DEBUG  
//#define TRACE  
#undef TRACE  
  
using System;  
  
public class TestDefine  
{  
    static void Main()  
    {  
#if (DEBUG)  
        Console.WriteLine("Debugging is enabled.");  
#endif  
  
#if (TRACE)  
     Console.WriteLine("Tracing is enabled.");  
#endif  
    }  
}  
// Output:  
// Debugging is enabled.  
```  
  
 有关如何取消定义符号的示例，请参见 [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md)。  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)   
 [const](../../../csharp/language-reference/keywords/const.md)   
 [How to: Compile Conditionally with Trace and Debug](../Topic/How%20to:%20Compile%20Conditionally%20with%20Trace%20and%20Debug.md)   
 [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md)   
 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)