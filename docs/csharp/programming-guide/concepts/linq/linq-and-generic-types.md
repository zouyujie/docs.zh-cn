---
title: "LINQ and Generic Types (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "LINQ [C#], generic types"
  - "generic types [LINQ]"
  - "generics [LINQ]"
ms.assetid: 660e3799-25ca-462c-8c4a-8bce04fbb031
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# LINQ and Generic Types (C#)
[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询基于泛型类型，在 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 的 2.0 版中引入了泛型类型。  您无需深入了解泛型即可开始编写查询。  但是，您可能需要了解两个基本概念：  
  
1.  当您创建泛型集合类（如 <xref:System.Collections.Generic.List%601>）的实例时，您将“T”替换为列表将包含的对象的类型。  例如，字符串列表表示为 `List<string>`，`Customer` 对象列表表示为 `List<Customer>`。  泛型列表是强类型的，且提供了比将其元素存储为 <xref:System.Object> 的集合更多的好处。  如果您尝试将 `Customer` 添加到 `List<string>`，则会在编译时出现一条错误。  泛型集合易于使用的原因是您不必执行运行时类型强制转换。  
  
2.  <xref:System.Collections.Generic.IEnumerable%601> 是一个接口，通过该接口，可以使用 `foreach` 语句来枚举泛型集合类。  泛型集合类支持 <xref:System.Collections.Generic.IEnumerable%601>，就像非泛型集合类（如 <xref:System.Collections.ArrayList>）支持 <xref:System.Collections.IEnumerable>。  
  
 有关泛型的更多信息，请参见[泛型](../../../../csharp/programming-guide/generics/index.md)。  
  
## LINQ 查询中的 IEnumerable\<T\> 变量  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询变量类型化为 <xref:System.Collections.Generic.IEnumerable%601> 或派生类型，如 <xref:System.Linq.IQueryable%601>。  当您看到类型化为 `IEnumerable<Customer>` 的查询变量时，这只意味着在执行该查询时，该查询将生成包含零个或多个 `Customer` 对象的序列。  
  
 [!code-cs[csLINQGettingStarted#34](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/linq-and-generic-types_1.cs)]  
  
 有关更多信息，请参见[Type Relationships in LINQ Query Operations](../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)。  
  
## 让编译器处理泛型类型声明  
 如果您愿意，可以使用 [var](../../../../csharp/language-reference/keywords/var.md) 关键字来避免使用泛型语法。  `var` 关键字指示编译器通过查看在 `from` 子句中指定的数据源来推断查询变量的类型。  下面的示例生成与上一个示例相同的编译代码：  
  
 [!code-cs[csLINQGettingStarted#35](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/linq-and-generic-types_2.cs)]  
  
 当变量的类型明显或显式指定嵌套泛型类型（如由组查询生成的那些类型）并不重要时，`var` 关键字很有用。  通常，我们建议如果您使用 `var`，应意识到这可能使您的代码更难以让别人理解。  有关更多信息，请参见[隐式类型的局部变量](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
## 请参阅  
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [泛型](../../../../csharp/programming-guide/generics/index.md)