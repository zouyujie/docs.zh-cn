---
title: "泛型（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, Generics — 泛型"
  - "泛型 [C#]"
ms.assetid: 75ea8509-a4ea-4e7a-a2b3-cf72482e9282
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# 泛型（C# 编程指南）
2.0 版 C\# 语言和公共语言运行时 \(CLR\) 中增加了泛型。  泛型将类型参数的概念引入 .NET Framework，类型参数使得设计如下类和方法成为可能：这些类和方法将一个或多个类型的指定推迟到客户端代码声明并实例化该类或方法的时候。  例如，通过使用泛型类型参数 T，您可以编写其他客户端代码能够使用的单个类，而不致引入运行时强制转换或装箱操作的成本或风险，如下所示：  
  
 [!code-cs[csProgGuideGenerics#1](../../../csharp/programming-guide/generics/codesnippet/CSharp/index_1.cs)]  
  
## 泛型概述  
  
-   使用泛型类型可以最大限度地重用代码、保护类型的安全以及提高性能。  
  
-   泛型最常见的用途是创建集合类。  
  
-   .NET Framework 类库在 <xref:System.Collections.Generic> 命名空间中包含几个新的泛型集合类。  应尽可能地使用这些类来代替普通的类，如 <xref:System.Collections> 命名空间中的 <xref:System.Collections.ArrayList>。  
  
-   您可以创建自己的泛型接口、泛型类、泛型方法、泛型事件和泛型委托。  
  
-   可以对泛型类进行约束以访问特定数据类型的方法。  
  
-   关于泛型数据类型中使用的类型的信息可在运行时通过使用反射获取。  
  
## 相关章节  
 有关更多信息：  
  
-   [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)  
  
-   [泛型的优点](../../../csharp/programming-guide/generics/benefits-of-generics.md)  
  
-   [泛型类型参数](../../../csharp/programming-guide/generics/generic-type-parameters.md)  
  
-   [类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)  
  
-   [泛型类](../../../csharp/programming-guide/generics/generic-classes.md)  
  
-   [泛型接口](../../../csharp/programming-guide/generics/generic-interfaces.md)  
  
-   [泛型方法](../../../csharp/programming-guide/generics/generic-methods.md)  
  
-   [泛型委托](../../../csharp/programming-guide/generics/generic-delegates.md)  
  
-   [default 关键字](../../../csharp/programming-guide/generics/default-keyword-in-generic-code.md)  
  
-   [C\+\+ 模板和 C\# 泛型之间的区别](../../../csharp/programming-guide/generics/differences-between-cpp-templates-and-csharp-generics.md)  
  
-   [泛型和反射](../../../csharp/programming-guide/generics/generics-and-reflection.md)  
  
-   [运行时中的泛型](../../../csharp/programming-guide/generics/generics-in-the-run-time.md)  
  
-   [.NET Framework 类库中的泛型](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md)  
  
## C\# 语言规范  
 有关更多信息，请参见 [C\# 语言规范](../../../csharp/language-reference/language-specification.md)。  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类型](../../../csharp/programming-guide/types/index.md)   
 [\<typeparam\>](../../../csharp/programming-guide/xmldoc/typeparam.md)   
 [\<typeparamref\>](../../../csharp/programming-guide/xmldoc/typeparamref.md)