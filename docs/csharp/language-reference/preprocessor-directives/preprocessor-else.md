---
title: "#else（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#else"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#else 指令 [C#]"
ms.assetid: 6a347322-cfa2-4a86-98f8-ddfa2cb7d4db
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# #else（C# 参考）
`#else` 允许您创建复合条件指令，因此，如果前面的 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 或（可选）[\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md) 指令中的任何表达式都不为 `true`，则编译器将计算 `#else` 与后面的 `#endif` 之间的所有代码。  
  
## 备注  
 [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md) 必须是 `#else` 之后的下一条预处理器指令。  有关如何使用 `#else` 的示例，请参见 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)