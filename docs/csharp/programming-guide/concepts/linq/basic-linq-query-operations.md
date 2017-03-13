---
title: "Basic LINQ Query Operations (C#) | Microsoft Docs"
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
  - "orderby clause [LINQ in C#]"
  - "ordering data [LINQ in C#]"
  - "selecting data [LINQ in C#]"
  - "queries [LINQ in C#], basic operations"
  - "grouping data [LINQ in C#]"
  - "data sources [LINQ in C#]"
  - "sorting data [LINQ in C#]"
  - "projections [LINQ in C#]"
  - "filtering data [LINQ in C#]"
  - "joining data [LINQ in C#]"
  - "select clause [LINQ in C#]"
  - "LINQ [C#], basic query operations"
  - "join clause [LINQ in C#]"
  - "group clause [LINQ in C#]"
ms.assetid: a7ea3421-1cf4-4df7-832a-aa22fe6379e9
caps.latest.revision: 39
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 37
---
# Basic LINQ Query Operations (C#)
本主题简要介绍 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询表达式，以及您在查询中执行的一些典型类型的操作。  下面各主题中提供了更详细的信息：  
  
 [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)  
  
 [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)  
  
 [Walkthrough: Writing Queries in C\#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)  
  
> [!NOTE]
>  如果您已熟悉查询语言（如 SQL 或 XQuery），则可以跳过本主题的大部分内容。  阅读下一节中的“`from` 子句”来了解 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询表达式中的子句的顺序。  
  
## 获取数据源  
 在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询中，第一步是指定数据源。  像在大多数编程语言中一样，在 C\# 中，必须先声明变量，才能使用它。  在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询中，最先使用 `from` 子句的目的是引入数据源 \(`customers`\) 和范围变量 \(`cust`\)。  
  
 [!code-cs[csLINQGettingStarted#23](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_1.cs)]  
  
 范围变量类似于 `foreach` 循环中的迭代变量，但在查询表达式中，实际上不发生迭代。  执行查询时，范围变量将用作对 `customers` 中的每个后续元素的引用。  因为编译器可以推断 `cust` 的类型，所以您不必显式指定此类型。  其他范围变量可由 `let` 子句引入。  有关更多信息，请参见[let 子句](../../../../csharp/language-reference/keywords/let-clause.md)。  
  
> [!NOTE]
>  对于非泛型数据源（如 <xref:System.Collections.ArrayList>），必须显式类型化范围变量。  有关更多信息，请参见[How to: Query an ArrayList with LINQ](../Topic/How%20to:%20Query%20an%20ArrayList%20with%20LINQ.md)和[from 子句](../../../../csharp/language-reference/keywords/from-clause.md)。  
  
## 筛选  
 也许最常用的查询操作是应用布尔表达式形式的筛选器。  此筛选器使查询只返回那些表达式结果为 true 的元素。  使用 `where` 子句生成结果。  实际上，筛选器指定从源序列中排除哪些元素。  在下面的示例中，只返回那些地址位于伦敦的 `customers`。  
  
 [!code-cs[csLINQGettingStarted#24](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_2.cs)]  
  
 您可以使用熟悉的 C\# 逻辑 `AND` 和 `OR` 运算符来根据需要在 `where` 子句中应用任意数量的筛选表达式。  例如，若要只返回位于“伦敦”`AND` 姓名为“Devon”的客户，您应编写下面的代码：  
  
 [!code-cs[csLINQGettingStarted#25](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_3.cs)]  
  
 若要返回位于伦敦或巴黎的客户，您应编写下面的代码：  
  
 [!code-cs[csLINQGettingStarted#26](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_4.cs)]  
  
 有关更多信息，请参见[where 子句](../../../../csharp/language-reference/keywords/where-clause.md)。  
  
## Ordering  
 通常可以很方便地将返回的数据进行排序。  `orderby` 子句将使返回的序列中的元素按照被排序的类型的默认比较器进行排序。  例如，下面的查询可以扩展为按 `Name` 属性对结果进行排序。  因为 `Name` 是一个字符串，所以默认比较器执行从 A 到 Z 的字母排序。  
  
 [!code-cs[csLINQGettingStarted#27](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_5.cs)]  
  
 若要按相反顺序（从 Z 到 A）对结果进行排序，请使用 `orderby…descending` 子句。  
  
 有关更多信息，请参见[orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。  
  
## 分组  
 使用 `group` 子句，您可以按指定的键分组结果。  例如，您可以指定结果应按 `City` 分组，以便位于伦敦或巴黎的所有客户位于各自组中。  在本例中，`cust.City` 是键。  
  
 [!code-cs[csLINQGettingStarted#28](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_6.cs)]  
  
 在使用 `group` 子句结束查询时，结果采用列表的列表形式。  列表中的每个元素是一个具有 `Key` 成员及根据该键分组的元素列表的对象。  在循环访问生成组序列的查询时，您必须使用嵌套的 `foreach` 循环。  外部循环用于循环访问每个组，内部循环用于循环访问每个组的成员。  
  
 如果您必须引用组操作的结果，可以使用 `into` 关键字来创建可进一步查询的标识符。  下面的查询只返回那些包含两个以上的客户的组：  
  
 [!code-cs[csLINQGettingStarted#29](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_7.cs)]  
  
 有关更多信息，请参见[group 子句](../../../../csharp/language-reference/keywords/group-clause.md)。  
  
## 联接  
 联接运算创建数据源中没有显式建模的序列之间的关联。  例如，您可以执行联接来查找位于同一地点的所有客户和经销商。  在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 中，`join` 子句始终针对对象集合而非直接针对数据库表运行。  
  
 [!code-cs[csLINQGettingStarted#36](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_8.cs)]  
  
 在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 中，您不必像在 SQL 中那样频繁使用 `join`，因为 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 中的外键在对象模型中表示为包含项集合的属性。  例如，`Customer` 对象包含 `Order` 对象的集合。  不必执行联接，只需使用点表示法访问订单：  
  
```  
from order in Customer.Orders...  
```  
  
 有关更多信息，请参见[join 子句](../../../../csharp/language-reference/keywords/join-clause.md)。  
  
## 选择（投影）  
 `select` 子句生成查询结果并指定每个返回的元素的“形状”或类型。  例如，您可以指定结果包含的是整个 `Customer` 对象、仅一个成员、成员的子集，还是某个基于计算或新对象创建的完全不同的结果类型。  当 `select` 子句生成除源元素副本以外的内容时，该操作称为“投影”。  使用投影转换数据是 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询表达式的一种强大功能。  有关更多信息，请参见[使用 LINQ 进行数据转换 \(C\#\)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md)和[select 子句](../../../../csharp/language-reference/keywords/select-clause.md)。  
  
## 请参阅  
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Walkthrough: Writing Queries in C\#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [查询关键字 \(LINQ\)](../../../../csharp/language-reference/keywords/query-keywords.md)   
 [匿名类型](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [基本查询操作 \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md)