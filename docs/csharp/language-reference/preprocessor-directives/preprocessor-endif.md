---
title: "#endif（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#endif"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#endif 指令 [C#]"
ms.assetid: 6a5fca55-5aee-441f-86f6-1c99fbe9ec05
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# #endif（C# 参考）
`#endif` 指定以 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) 指令开头的条件指令的结尾。  例如，  
  
```  
  
      #define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
## 备注  
 以 `#if` 指令开始的条件指令必须用 `#endif` 指令显式终止。  有关如何使用 `#endif` 的示例，请参见 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 预处理器指令](../../../csharp/language-reference/preprocessor-directives/index.md)