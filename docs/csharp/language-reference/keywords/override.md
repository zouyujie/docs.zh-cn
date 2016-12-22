---
title: "override（C# 参考） | Microsoft Docs"
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
  - "override"
  - "override_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "override 关键字 [C#]"
ms.assetid: dd1907a8-acf8-46d3-80b9-c2ca4febada8
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# override（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

要扩展或修改继承的方法、属性、索引器或事件的抽象实现或虚实现，必须使用 `override` 修饰符。  
  
## 示例  
 在此示例中，`Square` 类必须提供 `Area` 的重写实现，因为 `Area` 继承自抽象的 `ShapesClass`：  
  
 [!code-cs[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/override_1.cs)]  
  
 `override` 方法提供从基类继承的成员的新实现。  由 `override` 声明重写的方法称为重写基方法。  重写的基方法必须与 `override` 方法具有相同的签名。  有关继承的信息，请参见[继承](../../../fsharp/language-reference/inheritance.md)。  
  
 不能重写非虚方法或静态方法。  重写的基方法必须是 `virtual`、`abstract` 或 `override` 的。  
  
 `override` 声明不能更改 `virtual` 方法的可访问性。  `override` 方法和 `virtual` 方法必须具有相同的[访问级别修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 您不能使用 `new`、`static` 或 `virtual` 修饰符来修改 `override` 方法。  
  
 重写属性声明必须指定与继承属性完全相同的访问修饰符、类型和名称，并且被重写的属性必须是 `virtual`、`abstract` 或 `override` 的。  
  
 有关如何使用 `override` 关键字的更多信息，请参见[使用 Override 和 New 关键字进行版本控制](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)和[了解何时使用 Override 和 New 关键字](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)。  
  
## 示例  
 此示例定义了一个名为 `Employee` 的基类和一个名为 `SalesEmployee` 的派生类。  `SalesEmployee` 类包括一个额外的属性 `salesbonus`，并重写方法 `CalculatePay` 以便将该属性考虑在内。  
  
 [!code-cs[csrefKeywordsModifiers#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/override_2.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [继承](../../../fsharp/language-reference/inheritance.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [abstract](../../../csharp/language-reference/keywords/abstract.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [多态性](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)