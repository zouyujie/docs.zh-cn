---
title: "#undef（C# 参考） | Microsoft Docs"
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
  - "#undef"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#undef 指令 [C#]"
ms.assetid: 686c92d2-7194-4be4-b2f4-80091712d513
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #undef（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`#undef` 使您可以取消符号的定义，以便通过将该符号用作 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 指令中的表达式，使表达式的计算结果为 `false`。  
  
 可以使用 [\#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) 指令或 [\/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md) 编译器选项定义符号。  在使用任何不是指令的语句之前，必须在文件中使用 `#undef` 指令。  
  
## 示例  
  
```  
// preprocessor_undef.cs  
// compile with: /d:DEBUG  
#undef DEBUG  
using System;  
class MyClass   
{  
    static void Main()   
    {  
#if DEBUG  
        Console.WriteLine("DEBUG is defined");  
#else  
        Console.WriteLine("DEBUG is not defined");  
#endif  
    }  
}  
```  
  
  **未定义 DEBUG**   
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)