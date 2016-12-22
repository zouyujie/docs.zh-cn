---
title: "编写第一个 LINQ 查询 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic 中的 LINQ], 编写"
  - "LINQ 查询 [Visual Basic]"
  - "LINQ [Visual Basic], 编写查询"
ms.assetid: 4affb732-3e9b-4479-aa31-1f9bd8183cbe
caps.latest.revision: 56
caps.handback.revision: 54
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 编写第一个 LINQ 查询 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

查询是一种从数据源检索数据的表达式。  查询用专用查询语言表示。  随着时间的推移，人们已经为不同类型的数据源开发了不同的语言，例如，用于关系数据库的 SQL 和用于 XML 的 XQuery。  这使应用程序开发人员必须针对所支持的每种数据源或数据格式而学习新的查询语言。  
  
 [!INCLUDE[vbteclinqext](../../../../csharp/programming-guide/concepts/linq/includes/vbteclinqext_md.md)] 通过提供一种跨各种数据源和数据格式使用数据的一致模型，简化了这一情况。  在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询中，始终会用到对象。  在查询和转换 XML 文档、SQL 数据库、ADO.NET 数据集和实体、.NET Framework 集合中的数据以及具有相应的 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 提供程序的任何其他源或格式的数据时，都会使用相同的基本编码模式。  本文档描述创建和使用基本 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询的三个阶段。  
  
 ![链接到视频](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") 若要观看相关的视频演示，请参见 [How Do I: Get Started with LINQ?](http://go.microsoft.com/fwlink/?LinkId=133021)（如何实现：LINQ 入门）。  
  
## 查询操作的三个阶段  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询操作由以下三个操作组成：  
  
1.  获取数据源。  
  
2.  创建查询。  
  
3.  执行查询。  
  
 在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 中，执行查询与创建查询截然不同。  如果只是创建查询，则不会检索任何数据。  这一点将在本主题后面部分进行更详细的讨论。  
  
 下面的示例演示查询操作的三个部分。  出于演示的目的，此示例将一个整数数组用作简便的数据源。  但其中涉及的概念同样适用于其他数据源。  
  
> [!NOTE]
>  在 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)，请确保 **option infer** 设置为。  
  
 [!code-vb[VbLINQFirstQuery#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 输出：  
  
 `0 2 4 6`  
  
## 数据源  
 由于上一个示例中的数据源是数组，因此它隐式支持泛型 <xref:System.Collections.Generic.IEnumerable%601> 接口。  这一事实使您可以将数组用作 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询的数据源。  支持 <xref:System.Collections.Generic.IEnumerable%601> 或派生接口 \(如泛型 <xref:System.Linq.IQueryable%601> 的类型称为"可查询 *类型*"。  
  
 作为隐式可查询类型，该数组不需要进行修改或特殊处理就可以用作 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 数据源。  上述情况同样适用于支持 <xref:System.Collections.Generic.IEnumerable%601>，包括泛型 <xref:System.Collections.Generic.List%601>，<xref:System.Collections.Generic.Dictionary%602>的任何集合类型，因此，在 .NET framework 的其他选件类库。  
  
 如果源数据未实现 <xref:System.Collections.Generic.IEnumerable%601>，[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 提供程序需要的实现 *标准查询运算符的* 功能该数据源的。  例如，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 处理将 XML 文档加载到可查询的 <xref:System.Xml.Linq.XElement> 类型中的工作，如下面的示例所示。  有关标准查询运算符的更多信息，请参见[Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
 [!code-vb[VbLINQFirstQuery#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_2.vb)]  
  
 在 [!INCLUDE[vbtecdlinq](../../../../csharp/language-reference/keywords/includes/vbtecdlinq_md.md)] 中，首先手动或使用 [对象关系设计器（O\/R 设计器）](/visual-studio/data-tools/linq-to-sql-tools-in-visual-studio2) 在设计时创建对象关系映射。  针对这些对象编写查询，然后由 [!INCLUDE[vbtecdlinq](../../../../csharp/language-reference/keywords/includes/vbtecdlinq_md.md)] 在运行时处理与数据库的通信。  在下面的示例中，`customers` 表示数据库中的特定表，并且 <xref:System.Data.Linq.Table%601> 支持泛型 <xref:System.Linq.IQueryable%601> 接口。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 有关如何创建特定类型的数据源的更多信息，请参见各种 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 提供程序的文档。  （有关这些提供程序的列表，请参见[LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)。）基本规则很简单：[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 数据源是支持泛型 <xref:System.Collections.Generic.IEnumerable%601> 接口或从该接口继承的接口的任意对象。  
  
> [!NOTE]
>  支持非泛型 <xref:System.Collections.IEnumerable> 接口的类型（如 <xref:System.Collections.ArrayList>）也可用作 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 数据源。  有关使用 <xref:System.Collections.ArrayList> 的示例，请参见[How to: Query an ArrayList with LINQ](../Topic/How%20to:%20Query%20an%20ArrayList%20with%20LINQ.md)。  
  
## 查询  
 在查询中，指定要从数据源中检索的信息。  还可以指定在返回这些信息之前如何对其进行排序、分组或结构化。  为了便于创建查询，Visual Basic 语言中引入了新的查询语法。  
  
 下面示例中的查询在执行时从整数数组 `numbers` 返回所有偶数。  
  
 [!code-vb[VbLINQFirstQuery#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 该查询表达式包含三个子句：`From`、`Where` 和 `Select`。  其中每个查询表达式子句的具体功能和用途都在[基本查询操作 \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md) 中进行了讨论。  有关更多信息，请参见[查询](../../../../visual-basic/language-reference/queries/queries.md)。  请注意，在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 中，查询定义通常存储在变量中，并在以后执行。  查询变量，如前面示例中的 `evensQuery`，必须为可查询类型。`evensQuery` 的类型是 `IEnumerable(Of Integer)`，分配由使用局部类型推理的编译器。  
  
 有一点必须记住，就是查询变量本身不会执行任何操作，也不会返回任何数据。  它只是存储查询定义。  在上一个示例中，查询是由 `For Each` 执行的。  
  
## 查询执行  
 查询执行与查询创建不同。  查询创建过程定义查询，而查询执行由不同的机制触发。  可在定义查询后立即执行查询（“立即执行”），也可以存储查询定义，并在以后执行查询（“延迟执行”）。  
  
### 延迟执行  
 典型的 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询与上一个示例（其中定义了 `evensQuery`）中的查询类似。  该示例创建了查询，但并未立即执行它。  相反，查询定义被存储在查询变量 `evensQuery` 中。  可以在以后执行该查询，这通常需要使用 `For Each` 循环（它返回值序列）或应用标准查询运算符（如 `Count` 或 `Max`）。  此过程称为“延迟执行”。  
  
 [!code-vb[VbLINQFirstQuery#7](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_3.vb)]  
  
 对于值序列，可使用 `For Each` 循环中的迭代变量（在上一个示例中为 `number`）访问所检索的数据。  由于查询变量 `evensQuery` 保存了查询定义而不是查询结果，因此可多次使用该查询变量随意执行查询。  例如，您的应用程序中可能有一个由单独的应用程序持续更新的数据库。  在创建从该数据库检索数据的查询后，可使用 `For Each` 循环反复执行该查询，每次都检索到最新数据。  
  
 下面的示例演示延迟执行的工作方式。  如上一个示例所述，在定义 `evensQuery2` 并用 `For Each` 循环执行该查询之后，数据源 `numbers` 中的某些元素会发生更改。  然后，另一个 `For Each` 循环再次运行`evensQuery2`。  因为 `For Each` 循环使用 `numbers` 中的新值再次执行了该查询，因此第二次执行的结果会有所不同。  
  
 [!code-vb[VbLINQFirstQuery#3](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_4.vb)]  
  
 输出：  
  
 `Evens in original array:`  
  
 `0 2 4 6`  
  
 `Evens in changed array:`  
  
 `0 10 2 22 8`  
  
### 立即执行  
 在延迟执行查询的过程中，查询定义存储在查询变量中以供以后执行。  在立即执行过程中，查询在定义时执行。  当应用需要访问查询结果的各个元素的方法时，就会触发执行。  通常使用能够返回单个值的标准查询运算符之一来强制立即执行。  `Count`、`Max`、`Average` 和 `First` 就属于标准查询运算符。  只要应用了这些标准查询运算符以便计算并返回单一实例结果，这些运算符就会立即执行查询。  有关返回单个值的标准查询运算符的更多信息，请参见[Aggregation Operations](../../../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md)、[Element Operations](../../../../visual-basic/programming-guide/concepts/linq/element-operations.md)和[Quantifier Operations](../../../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md)。  
  
 下面的查询返回一个整数数组中偶数的计数。  查询定义未保存，并且 `numEvens` 是简单的 `Integer`。  
  
 [!code-vb[VbLINQFirstQuery#4](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_5.vb)]  
  
 可以使用 `Aggregate` 方法获得相同结果。  
  
 [!code-vb[VbLINQFirstQuery#5](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_6.vb)]  
  
 还可通过对查询（立即执行）或查询变量（延迟执行）调用 `ToList` 或 `ToArray` 方法来强制执行查询，如下面的代码所示。  
  
 [!code-vb[VbLINQFirstQuery#6](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_7.vb)]  
  
 在上述示例中，`evensQuery3` 是查询变量，而 `evensList`和 `evensArray` 分别是列表和数组。  
  
 如果要立即执行查询并将结果缓存在单个集合对象中，则使用 `ToList` 或 `ToArray` 强制立即执行尤为有用。  有关这些方法的更多信息，请参见[Converting Data Types](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md)。  
  
 还可以使用 `IEnumerable` 方法（如 <xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A> 方法）执行查询。  
  
## 相关视频演示  
 [How Do I: Get Started with LINQ?](http://go.microsoft.com/fwlink/?LinkId=133021)（如何实现：LINQ 入门）  
  
 [Video How to: Writing Queries in Visual Basic](http://go.microsoft.com/fwlink/?LinkID=100356)（视频帮助主题：在 Visual Basic 中编写查询）  
  
## 请参阅  
 [Getting Started with LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [LINQ 示例](../Topic/LINQ%20Samples.md)   
 [O\/R 设计器概述](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio1.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)