---
title: "out（泛型修饰符）（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "协变, out 关键字 [C#]"
  - "out 关键字 [C#]"
ms.assetid: f8c20dec-a8bc-426a-9882-4076b1db1e00
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# out（泛型修饰符）（C# 参考）
对于泛型类型参数，`out` 关键字指定该类型参数是协变的。  可以在泛型接口和委托中使用 `out` 关键字。  
  
 通过协变，可以使用与泛型参数指定的派生类型相比，派生程度更大的类型。  这样可以对委托类型和实现变体接口的类进行隐式转换。  引用类型支持协变和逆变，但值类型不支持。  
  
 如果接口具有协变类型形参，则允许其方法返回与接口类型形参指定的派生类型相比，派生程度更大的类型的实参。  例如，由于在 .NET Framework 4 的 <xref:System.Collections.Generic.IEnumerable%601> 接口中，类型 T 是协变的，因此无需使用任何特殊转换方法就可以将 `IEnumerabe(Of String)` 类型的对象分配给 `IEnumerable(Of Object)` 类型的对象。  
  
 可以向协变委托分配同一类型的其他委托，但需使用派生程度较大的泛型类型参数。  
  
 有关更多信息，请参见[协变和逆变](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 示例  
 下例演示如何声明、扩展和实现一个协变泛型接口。  此外还演示了如何对实现协变接口的类使用隐式转换。  
  
 [!code-cs[csVarianceKeywords#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-generic-modifier_1.cs)]  
  
 在泛型接口中，当符合下列条件时，可以将类型参数声明为是协变的。  
  
-   类型形参仅用作接口方法的返回类型，不用作方法实参的类型。  
  
    > [!NOTE]
    >  此规则有一个例外。  如果在协变接口中，包含用作方法参数的逆变泛型委托，则可以将协变类型用作此委托的泛型类型参数。  有关协变和逆变泛型委托的更多信息，请参见[委托中的变体](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)和[对 Func 和 Action 泛型委托使用变体](../Topic/Using%20Variance%20for%20Func%20and%20Action%20Generic%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)。  
  
-   类型参数不用作接口方法的泛型约束。  
  
## 示例  
 下例演示如何声明、实例化和调用一个协变泛型委托。  此外还演示了如何隐式转换委托类型。  
  
 [!code-cs[csVarianceKeywords#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-generic-modifier_2.cs)]  
  
 在泛型委托中，如果类型仅用作方法返回类型，且不用于方法参数，则可声明为是协变的。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [泛型接口中的变体](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [in](../../../csharp/language-reference/keywords/in-generic-modifier.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)