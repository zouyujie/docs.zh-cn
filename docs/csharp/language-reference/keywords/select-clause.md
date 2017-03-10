---
title: "select 子句（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "select_CSharpKeyword"
  - "select"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "select 子句 [C#]"
  - "select 关键字 [C#]"
ms.assetid: df01e266-5781-4aaa-80c4-67cf28ea093f
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# select 子句（C# 参考）
在查询表达式中，`select` 子句可以指定将在执行查询时产生的值的类型。  该子句的结果将基于前面所有子句的计算结果以及 `select` 子句本身中的所有表达式。  查询表达式必须以 `select` 子句或 [group](../../../csharp/language-reference/keywords/group-clause.md) 子句结束。  
  
 下面的示例演示了查询表达式中的简单 `select` 子句。  
  
 [!code-cs[cscsrefQueryKeywords#8](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Select.cs#8)]  
  
 `select` 子句产生的序列的类型决定了查询变量 `queryHighScores` 的类型。  在最简单的情况下，`select` 子句仅指定范围变量。  这会使返回的序列包含与数据源具有相同类型的元素。  有关更多信息，请参见[Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)。  不过，`select` 子句还提供了一种功能强大的机制，可用于将源数据转换（或投影）为新类型。  有关更多信息，请参见 [使用 LINQ 进行数据转换 \(C\#\)](../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md)。  
  
## 示例  
 下面的示例演示了 `select` 子句可能采用的所有不同形式。  在每个查询中，请注意 `select` 子句和查询变量（`studentQuery1`、`studentQuery2` 等）的类型之间的关系。  
  
 [!code-cs[cscsrefQueryKeywords#9](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Select.cs#9)]  
  
 如上一个示例中的 `studentQuery8` 所示，您有时可能希望所返回序列中的元素仅包含源元素的属性子集。  通过使返回的序列尽可能地小一些，可以降低内存需求，并提高查询的执行速度。  通过在 `select` 子句中创建一个匿名类型，并且借助于对象初始值设定项用源元素中的适当属性对该匿名类型进行初始化，可以达到此目的。  有关如何执行此操作的示例，请参见[对象和集合初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)。  
  
## 备注  
 编译时，`select` 子句会被转换为对 <xref:System.Linq.Enumerable.Select%2A> 标准查询运算符的方法调用。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [from 子句](../../../csharp/language-reference/keywords/from-clause.md)   
 [分部（方法）（C\# 参考）](../../../csharp/language-reference/keywords/partial-method.md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)