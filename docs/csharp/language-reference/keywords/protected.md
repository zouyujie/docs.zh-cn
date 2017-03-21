---
title: "protected（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "protected"
  - "protected_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "protected 关键字 [C#]"
ms.assetid: 05ce3794-6675-4025-bddb-eaaa0ec22892
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# protected（C# 参考）
`protected` 关键字是一个成员访问修饰符。  受保护成员在其所在的类中可由派生类实例访问。  有关 `protected` 与其他访问修饰符的比较，请参见[可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)。  
  
## 示例  
 只有在通过派生类类型发生访问时，基类的受保护成员在派生类中才是可访问的。  例如，请看以下代码段：  
  
 [!code-cs[csrefKeywordsModifiers#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/protected_1.cs)]  
  
 语句 `a.x = 10` 生成错误，因为它是在静态方法 Main 中生成的，而不是类 B 的实例。  
  
 结构成员无法受保护，因为无法继承结构。  
  
## 示例  
 此示例中，`DerivedPoint` 类派生自 `Point`。  因此，可以从派生类直接访问基类的受保护成员。  
  
 [!code-cs[csrefKeywordsModifiers#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/protected_2.cs)]  
  
 如果将 `x` 和 `y` 的访问级别更改为 [private](../../../csharp/language-reference/keywords/private.md)，编译器将发出错误信息：  
  
 `'Point.y' is inaccessible due to its protection level.`  
  
 `'Point.x' is inaccessible due to its protection level.`  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [访问修饰符](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [可访问性级别](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [内部](../../../csharp/language-reference/keywords/internal.md)