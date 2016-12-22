---
title: "泛型类型参数（C# 编程指南） | Microsoft Docs"
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
  - "泛型 [C#], 类型参数"
  - "类型参数 [C#]"
ms.assetid: a03b0ab2-0606-4b41-b7bf-e64d5bb4d18f
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 泛型类型参数（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在泛型类型或方法定义中，类型参数是客户端在实例化泛型类型的变量时指定的特定类型的占位符。  泛型类（如 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md) 中列出的 `GenericList<T>`）不可以像这样使用，因为它实际上并不是一个类型，而更像是一个类型的蓝图。  若要使用 `GenericList<T>`，客户端代码必须通过指定尖括号中的类型参数来声明和实例化构造类型。  此特定类的类型参数可以是编译器识别的任何类型。  可以创建任意数目的构造类型实例，每个实例使用不同的类型参数，如下所示：  
  
 [!CODE [csProgGuideGenerics#7](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#7)]  
  
 在每个 `GenericList<T>` 实例中，类中出现的每个 `T` 都会在运行时替换为相应的类型参数。  通过这种替换方式，我们使用一个类定义创建了三个独立的类型安全的有效对象。  有关 CLR 如何执行此替换的更多信息，请参见[运行时中的泛型](../../../csharp/programming-guide/generics/generics-in-the-run-time.md)。  
  
## 类型参数命名准则  
  
-   **务必**使用描述性名称命名泛型类型参数，除非单个字母名称完全可以让人了解它表示的含义，而描述性名称不会有更多的意义。  
  
     [!CODE [csProgGuideGenerics#8](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#8)]  
  
-   **考虑**使用 T 作为具有单个字母类型参数的类型的类型参数名。  
  
     [!CODE [csProgGuideGenerics#9](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#9)]  
  
-   **务必**将“T”作为描述性类型参数名的前缀。  
  
     [!CODE [csProgGuideGenerics#10](../CodeSnippet/VS_Snippets_VBCSharp/csProgGuideGenerics#10)]  
  
-   **考虑**在参数名中指示对此类型参数的约束。  例如，可以将带有 `ISession` 约束的参数命名为 `TSession`。  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)   
 [C\+\+ 模板和 C\# 泛型之间的区别](../../../csharp/programming-guide/generics/differences-between-cpp-templates-and-csharp-generics.md)