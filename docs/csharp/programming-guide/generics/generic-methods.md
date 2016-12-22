---
title: "泛型方法（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "泛型 [C#], 方法"
ms.assetid: 673eeea2-4b48-4faa-9c4e-2e89449221b9
caps.latest.revision: 27
caps.handback.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 泛型方法（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

泛型方法是使用类型参数声明的方法，如下所示：  
  
 [!CODE [csProgGuideGenerics#22](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#22)]  
  
 下面的代码示例演示一种使用 `int` 作为类型参数的方法调用方式：  
  
 [!CODE [csProgGuideGenerics#23](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#23)]  
  
 也可以省略类型参数，编译器将推断出该参数。  下面对 `Swap` 的调用等效于前面的调用：  
  
 [!CODE [csProgGuideGenerics#24](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#24)]  
  
 相同的类型推理规则也适用于静态方法和实例方法。  编译器能够根据传入的方法实参推断类型形参；它无法仅从约束或返回值推断类型形参。  因此，类型推理不适用于没有参数的方法。  类型推理在编译时、编译器尝试解析重载方法签名之前进行。  编译器向共享相同名称的所有泛型方法应用类型推理逻辑。  在重载解析步骤中，编译器仅包括类型推理取得成功的那些泛型方法。  
  
 在泛型类中，非泛型方法可以访问类级别类型参数，如下所示：  
  
 [!CODE [csProgGuideGenerics#25](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#25)]  
  
 如果定义采用相同类型参数作为包含类的泛型方法，编译器将生成警告 CS0693，因为在方法范围内为内部 `T` 提供的参数隐藏了为外部 `T` 提供的参数。  如果需要使用其他类型参数（而不是实例化类时提供的类型参数）来灵活地调用泛型类方法，请考虑为方法的类型参数提供另一个标识符，如下面示例的 `GenericList2<T>` 中所示。  
  
 [!CODE [csProgGuideGenerics#26](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#26)]  
  
 使用约束对方法中的类型参数启用更专门的操作。  此版本的 `Swap<T>` 现在名为 `SwapIfGreater<T>`，它只能与实现 <xref:System.IComparable%601> 的类型参数一起使用。  
  
 [!CODE [csProgGuideGenerics#27](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#27)]  
  
 泛型方法可以使用许多类型参数进行重载。  例如，下列方法可以全部位于同一个类中：  
  
 [!CODE [csProgGuideGenerics#28](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#28)]  
  
## C\# 语言规范  
 有关更多信息，请参见 [C\# 语言规范](../../../csharp/language-reference/language-specification.md)。  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)