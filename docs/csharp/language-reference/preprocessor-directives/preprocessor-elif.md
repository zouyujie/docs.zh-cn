---
title: "#elif（C# 参考） | Microsoft Docs"
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
  - "#elif"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#elif 指令 [C#]"
ms.assetid: 731d78df-08e0-4d51-b8c8-f193c27de13f
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #elif（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`#elif` 使您得以创建复合条件指令。  如果之前的[\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 和任何之前的，可选的，`#elif` 关系表达式的值为`true`，则`#elif`表达式将被执行。  如果 `#elif` 表达式计算为 `true`，编译器将计算位于 `#elif` 和下一个条件指令之间的所有代码。  例如：  
  
```  
#define VC7  
//...  
#if debug  
    Console.Writeline("Debug build");  
#elif VC7  
    Console.Writeline("Visual Studio 7");  
#endif  
```  
  
 可以使用运算符 `==`（相等）、`!=`（不相等）、`&&`（与）及 `||`（或）来计算多个符号。  还可以用括号将符号和运算符分组。  
  
## 备注  
 `#elif` 等效于使用：  
  
```  
#else  
#if  
```  
  
 使用 `#elif` 更简单，因为每个 `#if` 都需要一个 [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md)，而 `#elif` 即使在没有匹配的 `#endif` 时也可以使用。  
  
 有关如何使用 `#elif` 的示例，请参见 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)。  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)