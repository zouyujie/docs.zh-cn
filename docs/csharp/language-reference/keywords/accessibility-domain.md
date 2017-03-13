---
title: "可访问域（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "可访问性域 [C#]"
ms.assetid: 8af779c1-275b-44be-a864-9edfbca71bcc
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# 可访问域（C# 参考）
成员的可访问域指定程序中可以引用成员的部分。  如果成员嵌套在其他类型中，其可访问域由该成员的[可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)和直接包含类型的可访问域共同确定。  
  
 顶级类型的可访问域至少是声明它的项目的程序文本。  也就是说，域包括此项目的所有源文件。  嵌套类型的可访问域至少是声明它的类型的程序文本，  即域是一个类型体，包括所有嵌套的类型。  嵌套类型的可访问域决不能超出包含类型的可访问域。  这些概念在以下示例中加以说明。  
  
## 示例  
 该示例包含一个顶级类型 `T1` 和两个嵌套类 `M1` 和 `M2`。  这两个类包含具有不同声明的可访问性的字段。  在 `Main` 方法中，每个语句后都有注释，指示每个成员的可访问域。  注意，尝试引用不可访问的成员的语句被注释掉了。  如果希望查看由引用不可访问的成员所导致的编译器错误，请逐个移除注释。  
  
 [!code-cs[csrefKeywordsModifiers#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/accessibility-domain_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [对使用可访问性级别的限制](../../../csharp/language-reference/keywords/restrictions-on-using-accessibility-levels.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)