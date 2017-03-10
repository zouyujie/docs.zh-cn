---
title: "Introduction to LINQ Queries (C#) | Microsoft Docs"
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
  - "deferred execution [LINQ]"
  - "LINQ, queries"
  - "LINQ, deferred execution"
  - "queries [LINQ], about LINQ queries"
ms.assetid: 37895c02-268c-41d5-be39-f7d936fa88a8
caps.latest.revision: 47
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 45
---
# Introduction to LINQ Queries (C#)
查询是一种从数据源检索数据的表达式。  查询通常用专门的查询语言来表示。  随着时间的推移，人们已经为各种数据源开发了不同的语言；例如，用于关系数据库的 SQL 和用于 XML 的 XQuery。  因此，开发人员不得不针对他们必须支持的每种数据源或数据格式而学习新的查询语言。  [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 通过提供一种跨各种数据源和数据格式使用数据的一致模型，简化了这一情况。  在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询中，始终会用到对象。  可以使用相同的基本编码模式来查询和转换 XML 文档、SQL 数据库、[!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado-md.md)] 数据集、.NET 集合中的数据以及对其有 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序可用的任何其他格式的数据。  
  
## 查询操作的三个部分  
 所有 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询操作都由以下三个不同的操作组成：  
  
1.  获取数据源。  
  
2.  创建查询。  
  
3.  执行查询。  
  
 下面的示例演示如何用源代码表示查询操作的三个部分。  为方便起见，此示例将一个整数数组用作数据源；但其中涉及的概念同样适用于其他数据源。  本主题的其余部分也会引用此示例。  
  
 [!code-cs[CsLINQGettingStarted#1](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#1)]  
  
 下图显示了完整的查询操作。  在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 中，查询的执行与查询本身截然不同；换句话说，如果只是创建查询变量，则不会检索任何数据。  
  
 ![完整的 LINQ 查询操作](../../../../csharp/programming-guide/concepts/linq/media/linq-query.png "LINQ\_Query")  
  
## 数据源  
 在上一个示例中，由于数据源是数组，因此它隐式支持泛型 <xref:System.Collections.Generic.IEnumerable%601> 接口。  这一事实意味着该数据源可以用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 进行查询。  查询在 `foreach` 语句中执行，因此，`foreach` 需要 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601>。  支持 <xref:System.Collections.Generic.IEnumerable%601> 或派生接口（如泛型 <xref:System.Linq.IQueryable%601>）的类型称为*可查询类型*。  
  
 可查询类型不需要进行修改或特殊处理就可以用作 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 数据源。  如果源数据还没有作为可查询类型出现在内存中，则 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序必须以此方式表示源数据。  例如，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 将 XML 文档加载到可查询的 <xref:System.Xml.Linq.XElement> 类型中：  
  
 [!code-cs[CsLINQGettingStarted#2](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#2)]  
  
 在 [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq-md.md)] 中，首先手动或使用 [对象关系设计器（O\/R 设计器）](/visual-studio/data-tools/linq-to-sql-tools-in-visual-studio2) 在设计时创建对象关系映射。  针对这些对象编写查询，然后由 [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq-md.md)] 在运行时处理与数据库的通信。  在下面的示例中，`Customers` 表示数据库中的特定表，并且查询结果的类型 <xref:System.Linq.IQueryable%601> 派生自 <xref:System.Collections.Generic.IEnumerable%601>。  
  
```c#  
Northwnd db = new Northwnd(@"c:\northwnd.mdf");  
  
// Query for customers in London.  
IQueryable<Customer> custQuery =  
    from cust in db.Customers  
    where cust.City == "London"  
    select cust;  
  
```  
  
 有关如何创建特定类型的数据源的更多信息，请参见各种 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序的文档。  但基本规则非常简单：[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 数据源是支持泛型 <xref:System.Collections.Generic.IEnumerable%601> 接口或从该接口继承的接口的任意对象。  
  
> [!NOTE]
>  支持非泛型 <xref:System.Collections.IEnumerable> 接口的类型（如 <xref:System.Collections.ArrayList>）也可用作 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 数据源。  有关详细信息，请参阅 [How to: Query an ArrayList with LINQ](../Topic/How%20to:%20Query%20an%20ArrayList%20with%20LINQ.md)。  
  
##  <a name="query"></a> 查询  
 查询指定要从数据源中检索的信息。  查询还可以指定在返回这些信息之前如何对其进行排序、分组和结构化。  查询存储在查询变量中，并用查询表达式进行初始化。  为使编写查询的工作变得更加容易，C\# 引入了新的查询语法。  
  
 上一个示例中的查询从整数数组中返回所有偶数。  该查询表达式包含三个子句：`from`、`where` 和 `select`。（如果您熟悉 SQL，您会注意到这些子句的顺序与 SQL 中的顺序相反。）`from` 子句指定数据源，`where` 子句应用筛选器，`select` 子句指定返回的元素的类型。  [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)一节中详细讨论了这些子句和其他查询子句。  目前需要注意的是，在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 中，查询变量本身不执行任何操作并且不返回任何数据。  它只是存储在以后某个时刻执行查询时为生成结果而必需的信息。  有关在幕后是如何构建查询的更多信息，请参见[Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
> [!NOTE]
>  还可以使用方法语法来表示查询。  有关详细信息，请参阅 [Query Syntax and Method Syntax in LINQ](../../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)。  
  
## 查询执行  
  
### 延迟执行  
 如前所述，查询变量本身只是存储查询命令。  实际的查询执行会延迟到在 `foreach` 语句中循环访问查询变量时发生。  此概念称为“延迟执行”，下面的示例对此进行了演示：  
  
 [!code-cs[csLinqGettingStarted#4](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#4)]  
  
 `foreach` 语句也是检索查询结果的地方。  例如，在上一个查询中，迭代变量 `num` 保存了返回的序列中的每个值（一次保存一个值）。  
  
 由于查询变量本身从不保存查询结果，因此可以根据需要随意执行查询。  例如，可以通过一个单独的应用程序持续更新数据库。  在应用程序中，可以创建一个检索最新数据的查询，并可以按某一时间间隔反复执行该查询以便每次检索不同的结果。  
  
### 强制立即执行  
 对一系列源元素执行聚合函数的查询必须首先循环访问这些元素。  `Count`、`Max`、`Average` 和 `First` 就属于此类查询。  由于查询本身必须使用 `foreach` 以便返回结果，因此这些查询在执行时不使用显式 `foreach` 语句。  另外还要注意，这些类型的查询返回单个值，而不是 `IEnumerable` 集合。  下面的查询返回源数组中偶数的计数：  
  
 [!code-cs[csLinqGettingStarted#5](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#5)]  
  
 若要强制立即执行任意查询并缓存其结果，可以调用 <xref:System.Linq.Enumerable.ToList%2A> 或 <xref:System.Linq.Enumerable.ToArray%2A> 方法。  
  
 [!code-cs[csLinqGettingStarted#6](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#6)]  
  
 此外，还可以通过在紧跟查询表达式之后的位置放置一个 `foreach` 循环来强制执行查询。  但是，通过调用 `ToList` 或 `ToArray`，也可以将所有数据缓存在单个集合对象中。  
  
## 请参阅  
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Walkthrough: Writing Queries in C\#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [LINQ 示例](../Topic/LINQ%20Samples.md)   
 [O\/R 设计器概述](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio1.md)   
 [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [foreach，in](../../../../csharp/language-reference/keywords/foreach-in.md)   
 [查询关键字 \(LINQ\)](../../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 和已推迟的视频执行](http://go.microsoft.com/fwlink/?LinkId=112414)