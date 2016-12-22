---
title: "#if（C# 参考） | Microsoft Docs"
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
  - "#if"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#if 指令 [C#]"
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #if（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

如果 C\# 编译器遇到最后面跟有 [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md) 指令的  `#if` 指令，则仅当指定的符号已定义时，它才会编译这两个指令之间的代码。  与 C 和 C\+\+ 不同，您不能对符号赋予数值；C\# 中的 \#if 语句是 Boolean，仅测试符号是否已定义。  例如，  
  
```  
#define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
 使用运算符 [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md)（相等）和 [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md)（不相等）只能测试出结果为 [true](../../../csharp/language-reference/keywords/true.md) 还是 [false](../../../csharp/language-reference/keywords/false.md)。  True 表示符号已定义。  语句 `#if DEBUG` 与 `#if (DEBUG == true)` 的含义相同。  可以使用运算符[&&](../../../csharp/language-reference/operators/conditional-and-operator.md) \(and\)、[&#124;&#124;](../Topic/%7C%7C%20Operator%20\(C%23%20Reference\).md) \(or\) 和 [\!](../../../csharp/language-reference/operators/logical-negation-operator.md)\(无\) 计算多个符号是否定义了。  还可以用括号将符号和运算符分组。  
  
## 备注  
 结合使用 `#if` 与 [\#else](../../../csharp/language-reference/preprocessor-directives/preprocessor-else.md)、[\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md)、[\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md)、[\#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) 和 [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md) 指令，可以根据一个或多个符号是否存在来包含或排除代码。  在编译调试版本的代码或针对特定配置进行编译时，这会很有用。  
  
 以 `#if` 指令开始的条件指令必须用 `#endif` 指令显式终止。  
  
 `#define` 使您可以定义一个符号，通过将该符号用作传递给 `#if` 指令的表达式，使该表达式计算为 `true`。  
  
 也可以用 [\/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md) 编译器选项来定义符号。  可以用 [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md) 来取消定义符号。  
  
 用 `/define` 或 `#define` 定义的符号与具有同一名称的变量不冲突。  即，不应将变量名传递到预处理器指令，并且只能用预处理器指令计算符号。  
  
 用 `#define` 创建的符号的范围是在其中定义该符号的文件。  
  
## 示例  
  
```  
// preprocessor_if.cs  
#define DEBUG #define MYTEST  
using System;  
public class MyClass   
{  
    static void Main()   
    {  
#if (DEBUG && !MYTEST)  
        Console.WriteLine("DEBUG is defined");  
#elif (!DEBUG && MYTEST)  
        Console.WriteLine("MYTEST is defined");  
#elif (DEBUG && MYTEST)  
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else  
        Console.WriteLine("DEBUG and MYTEST are not defined");  
#endif  
    }  
}  
```  
  
  **定义 DEBUG 和 MYTEST**   
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)