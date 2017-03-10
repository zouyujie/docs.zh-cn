---
title: "in（泛型修饰符）（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "逆变, in 关键字 [C#]"
  - "in 关键字 [C#]"
ms.assetid: 3a778c36-8aed-4ebe-aa8b-39f4057215b1
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# in（泛型修饰符）（C# 参考）
对于泛型类型参数，`in` 关键字指定该类型参数是逆变的。  可以在泛型接口和委托中使用 `in` 关键字。  
  
 通过逆变，可以使用与泛型参数指定的派生类型相比，派生程度更小的类型。  这样可以对委托类型和实现变体接口的类进行隐式转换。  引用类型支持泛型类型参数中的协变和逆变，但值类型不支持。  
  
 在泛型接口或委托中，如果类型形参仅用作方法返回类型，而不用于方法实参，则可声明为协变的。  `Ref` 和 `out` 参数不能为变体。  
  
 如果接口具有逆变类型形参，则允许其方法接受与接口类型形参指定的派生类型相比，派生程度更小的类型的实参。  例如，由于在 .NET Framework 4 的 <xref:System.Collections.Generic.IComparer%601> 接口中，类型 T 是逆变的，因此如果 `Employee` 继承 `Person`，则无需使用任何特殊转换方法，就可以将 `IComparer(Of Person)` 类型的对象指派给 `IComparer(Of Employee)` 类型的对象。  
  
 可以向逆变委托分配同一类型的其他委托，但需使用派生程度较小的泛型类型参数。  
  
 有关更多信息，请参见[协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 示例  
 下例演示如何声明、扩展和实现一个逆变泛型接口。  此外还演示了如何对实现此接口的类使用隐式转换。  
  
 [!code-cs[csVarianceKeywords#1](../../../csharp/language-reference/keywords/codesnippet/csharp/in-generic-modifier_1.cs)]  
  
## 示例  
 下例演示如何声明、实例化和调用一个逆变泛型委托。  此外还演示了如何隐式转换委托类型。  
  
 [!code-cs[csVarianceKeywords#2](../../../csharp/language-reference/keywords/codesnippet/csharp/in-generic-modifier_2.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [out](../../../csharp/language-reference/keywords/out-generic-modifier.md)   
 [协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)