---
title: "Query Syntax and Method Syntax in LINQ (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "LINQ [C#], query syntax vs. method syntax"
  - "queries [LINQ in C#], syntax comparisons"
ms.assetid: eedd6dd9-fec2-428c-9581-5b8783810ded
caps.latest.revision: 30
caps.handback.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Query Syntax and Method Syntax in LINQ (C#)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

在表示语言集成查询 \([!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]\) 使用 LINQ 性查询语法，文档中的多数查询编写。  但是，在中，当编译代码时，必须将查询语法转换方法需要 .NET 公共语言运行时 \(CLR\)。  这些方法调用标准查询运算符，的名称类似 `Where`、`Select`、`GroupBy`、`Join`、`Max`和 `Average`。  可以调用这些方法直接使用方法语法而不是查询语法。  
  
 查询语法和方法语法语义相同的，但是，许多人员发现查询语法更简单、更易于阅读。  某些查询必须表示为方法调用。  例如，必须使用方法调用表示检索元素的数量与指定的条件的查询。  还必须使用方法需要检索元素的最大值在源序列的查询。  <xref:System.Linq> 命名空间中的标准查询运算符的参考文档通常使用方法语法。  因此，即使在开始编写 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询时，熟悉如何在查询和查询表达式本身中使用方法语法也非常有用。  
  
## 标准查询运算符扩展方法  
 下面的示例演示简单的查询表达式和编写为基于方法的查询的语义上等效的查询。  
  
 [!code-cs[csLINQGettingStarted#22](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/query-syntax-and-method-syntax-in-linq_1.cs)]  
  
 两个示例的输出是相同的。  您可以看到两种形式的查询变量的类型是相同的：<xref:System.Collections.Generic.IEnumerable%601>。  
  
 若要了解基于方法的查询，让我们进一步地分析它。  注意，在表达式的右侧，`where` 子句现在表示为对 `numbers` 对象的实例方法，在您重新调用该对象时其类型为 `IEnumerable<int>`。  如果您熟悉泛型 <xref:System.Collections.Generic.IEnumerable%601> 接口，那么您就会了解，它不具有 `Where` 方法。  但是，如果您在 Visual Studio IDE 中调用 IntelliSense 完成列表，那么您不仅将看到 `Where` 方法，而且还会看到许多其他方法，如 `Select`、`SelectMany`、`Join` 和 `Orderby`。  下面是所有标准查询运算符。  
  
 ![Intellisense 中的标准查询运算符](../../../../csharp/programming-guide/concepts/linq/media/standardqueryops.png "StandardQueryOps")  
  
 尽管看起来 <xref:System.Collections.Generic.IEnumerable%601> 似乎已被重新定义以包括这些附加方法，但事实上并非如此。  这些标准查询运算符作为一种新的方法（称为“扩展方法”）实现。  扩展方法可“扩展”现有类型；可如对类型的实例方法一样调用。  标准查询运算符可扩展 <xref:System.Collections.Generic.IEnumerable%601>，这就是您可以编写 `numbers.Where(...)` 的原因。  
  
 若要开始使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]，您实际需要了解的有关扩展方法的所有内容是，如何通过使用正确的 `using` 指令将它们置于您的应用程序中的范围内。  您可以在[How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)中进一步了解相关信息。  从应用程序的角度来看，扩展方法和正常的实例方法是相同的。  
  
 有关扩展方法的更多信息，请参见[扩展方法](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)。  有关标准查询运算符的更多信息，请参见[Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  一些 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 提供程序（如 [!INCLUDE[vbtecdlinq](../../../../csharp/language-reference/keywords/includes/vbtecdlinq_md.md)] 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]）除了 <xref:System.Collections.Generic.IEnumerable%601> 外，还为其他类型实现其自身的标准查询运算符和其他扩展方法。  
  
## Lambda 表达式  
 在前面的示例中，通知该条件表达式 \(`num % 2 == 0`\) 是作为内联参数。`Where` 方法：`Where(num => num % 2 == 0).`此内联表达式称为 lambda 表达式。  将代码编写为匿名方法或泛型委托或表达式树是一种便捷的方法，否则编写起来就要麻烦得多。  在 C\# 中，`=>` 是 lambda 运算符，可读为“goes to”。  运算符左侧的 `num` 是输入变量，与查询表达式中的 `num` 相对应。  编译器可推断 `num` 的类型，因为它了解 `numbers` 是泛型 <xref:System.Collections.Generic.IEnumerable%601> 类型。  lambda 表达式与查询语法中的表达式或任何其他 C\# 表达式或语句中的表达式相同；它可以包括方法调用和其他复杂逻辑。  “返回值”就是表达式结果。  
  
 若要开始使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]，您不必大量使用 lambda。  但是，特定查询只可使用方法语法表示，其中一些查询需要使用 lambda 表达式。  进一步熟悉 lambda 后，您会发现，在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 工具栏中，它们是强大且灵活的工具。  有关更多信息，请参见[Lambda 表达式](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
## 查询的组合性  
 在上面的代码示例中，请注意 `OrderBy` 方法是通过在对 `Where` 的调用中使用点运算符来调用的。  `Where` 生成筛选序列，然后 `Orderby` 通过对该序列排序来对它进行操作。  因为查询会返回 `IEnumerable`，所以您可通过将方法调用链接在一起，在方法语法中将这些查询组合起来。  这就是在您通过使用查询语法编写查询时编译器在后台所执行的操作。  并且由于查询变量不存储查询的结果，因此您可以随时修改它或将它用作新查询的基础，即使在执行它后。  
  
## 请参阅  
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)