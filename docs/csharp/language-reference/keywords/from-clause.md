---
title: "from 子句（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "from_CSharpKeyword"
  - "from"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "from 子句 [C#]"
  - "from 关键字 [C#]"
ms.assetid: 1aefd18c-1314-47f8-99ec-9bcefb09e699
caps.latest.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 27
---
# from 子句（C# 参考）
查询表达式必须以 `from` 子句开头。  另外，查询表达式还可以包含子查询，子查询也是以 `from` 子句开头。  `from` 子句指定以下内容：  
  
-   将对其运行查询或子查询的数据源。  
  
-   一个本地范围变量，表示源序列中的每个元素。  
  
 范围变量和数据源都是强类型。  `from` 子句中引用的数据源的类型必须为 <xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601> 或一种派生类型（如 <xref:System.Linq.IQueryable%601>）。  
  
 在下面的示例中，`numbers` 是数据源，而 `num` 是范围变量。  请注意，这两个变量都是强类型，即使使用了 [var](../../../csharp/language-reference/keywords/var.md) 关键字也是如此。  
  
 [!code-cs[cscsrefQueryKeywords#1](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/From.cs#1)]  
  
## 范围变量  
 如果数据源实现了 <xref:System.Collections.Generic.IEnumerable%601>，则编译器可以推断范围变量的类型。  例如，如果数据源的类型为 `IEnumerable<Customer>`，则推断出范围变量的类型为 `Customer`。  仅当数据源是非泛型 `IEnumerable` 类型（如 <xref:System.Collections.ArrayList>）时，才必须显式指定数据源类型。  有关更多信息，请参见 [How to: Query an ArrayList with LINQ](../Topic/How%20to:%20Query%20an%20ArrayList%20with%20LINQ.md)。  
  
 在上一个示例中，`num` 被推断为 `int` 类型。  由于范围变量是强类型，因此可以对其调用方法或者在其他操作中使用它。  例如，可以不编写 `select num`，而编写 `select num.ToString()` 使查询表达式返回一个字符串序列而不是整数序列。  或者，也可以编写 `select n + 10` 使表达式返回序列 14、11、13、12、10。  有关更多信息，请参见 [select 子句](../../../csharp/language-reference/keywords/select-clause.md)。  
  
 范围变量类似于 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 语句中的迭代变量，只是两者之间有一个非常重要的区别：范围变量从不实际存储来自数据源的数据。  范围变量只是提供了语法上的便利，使查询能够描述执行查询时将发生的事情。  有关更多信息，请参见 [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)。  
  
## 复合 from 子句  
 在某些情况下，源序列中的每个元素本身可能是序列，也可能包含序列。  例如，数据源可能是一个 `IEnumerable<Student>`，其中，序列中的每个 Student 对象都包含一个测验得分列表。  若要访问每个 `Student` 元素中的内部列表，可以使用复合 `from` 子句。  该技术类似于使用嵌套的 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 语句。  可以向任一 `from` 子句中添加 [where](../../../csharp/language-reference/keywords/partial-method.md) 或 [orderby](../../../csharp/language-reference/keywords/orderby-clause.md) 子句来筛选结果。  下面的示例演示了一个 `Student` 对象序列，其中每个对象都包含一个表示测验得分的内部整数 `List`。  为了访问该内部列表，此示例使用了复合 `from` 子句。  如有必要，可在两个 `from` 子句之间再插入子句。  
  
 [!code-cs[cscsrefQueryKeywords#2](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/From.cs#2)]  
  
## 使用多个 from 子句执行联接  
 复合 `from` 子句用于访问单个数据源中的内部集合。  不过，查询还可以包含多个可从独立数据源生成补充查询的 `from` 子句。  使用此技术可以执行某些类型的、无法通过使用 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)执行的联接操作。  
  
 下面的示例演示如何使用两个 `from` 子句构成两个数据源的完全交叉联接。  
  
 [!code-cs[cscsrefQueryKeywords#3](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/From.cs#3)]  
  
 有关使用多个 `from` 子句的联接操作的更多信息，请参见[如何：执行自定义联接操作](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md)。  
  
## 请参阅  
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)