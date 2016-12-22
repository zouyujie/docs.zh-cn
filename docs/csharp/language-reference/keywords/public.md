---
title: "public（C# 参考） | Microsoft Docs"
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
  - "public"
  - "public_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "public 关键字 [C#]"
ms.assetid: 0ae45d16-a551-4b74-9845-57208de1328e
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# public（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`public` 关键字是类型和类型成员的访问修饰符。  公共访问是允许的最高访问级别。  对访问公共成员没有限制，如下例所示：  
  
```  
class SampleClass  
{  
    public int x; // No access restrictions.  
}  
```  
  
 有关更多信息，请参见[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)和[可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)。  
  
## 示例  
 在下面的示例中，声明了两个类：`PointTest` 和 `MainClass`。  直接从 `MainClass` 访问 `PointTest` 的公共成员 `x` 和 `y`。  
  
 [!code-cs[csrefKeywordsModifiers#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/public_1.cs)]  
  
 如果将 `public` 访问级别更改为 [private](../../../csharp/language-reference/keywords/private.md) 或 [protected](../../../csharp/language-reference/keywords/protected.md)，您将收到错误信息：  
  
 “PointTest.y”不可访问，因为它受保护级别限制。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)