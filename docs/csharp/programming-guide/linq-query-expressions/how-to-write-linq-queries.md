---
title: "如何：在 C# 中编写 LINQ 查询 | Microsoft Docs"
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
  - "查询 [C# 中的 LINQ], 编写"
  - "查询表达式 [C# 中的 LINQ], 编写查询"
  - "编写 LINQ 查询"
ms.assetid: 45e47fcc-cfa1-4b72-b161-d038ae87bd23
caps.latest.revision: 25
caps.handback.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在 C# 中编写 LINQ 查询
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本主题演示在 C\# 中编写 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 查询的三种方式：  
  
1.  使用查询语法。  
  
2.  使用方法语法。  
  
3.  组合使用查询语法和方法语法。  
  
 下面的示例使用前面列出的每种方式演示一些简单的 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 查询。  一般的规则是尽可能使用 \(1\)，而在必要时使用 \(2\) 和 \(3\)。  
  
> [!NOTE]
>  这些查询作用于简单的内存中集合；但是，基本语法与 [!INCLUDE[vbtecdlinq](../../../csharp/language-reference/keywords/includes/vbtecdlinq_md.md)] 和 [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中使用的语法相同。  
  
## 示例  
  
## 查询语法  
 编写大多数查询的推荐方式是使用查询语法来创建查询表达式。  下面的示例演示了三个查询表达式。  第一个查询表达式演示如何通过用 `where` 子句应用条件来筛选或限制结果，  它返回源序列中值大于 7 或小于 3 的所有元素。  第二个表达式演示如何对返回的结果进行排序。  第三个表达式演示如何按照键对结果进行分组，  此查询可根据单词的第一个字母返回两个组。  
  
 [!code-cs[csProgGuideLINQ#5](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_1.cs)]  
  
 请注意，这些查询的类型是 <xref:System.Collections.Generic.IEnumerable%601>。  所有这些查询都可以使用 `var` 编写，如下面的示例所示：  
  
 `var query = from num in numbers...`  
  
 在上述每个示例中，直到您在 `foreach` 语句中循环访问查询变量时，查询才会实际执行。  有关更多信息，请参见 [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)。  
  
## 示例  
  
## 方法语法  
 某些查询操作必须表示为方法调用。  最常见的此类方法是那些返回单一数值的方法，如 <xref:System.Linq.Enumerable.Sum%2A>、<xref:System.Linq.Enumerable.Max%2A>、<xref:System.Linq.Enumerable.Min%2A>、<xref:System.Linq.Enumerable.Average%2A> 等。  这些方法在任何查询中都必须总是最后调用，因为它们仅表示单个值，不能充当其他查询操作的数据源。  下面的示例演示查询表达式中的方法调用：  
  
 [!code-cs[csProgGuideLINQ#6](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_2.cs)]  
  
## 示例  
 如果该方法具有参数，则这些参数以 [lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) 表达式的形式提供，如下面的示例所示：  
  
 [!code-cs[csProgGuideLINQ#7](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_3.cs)]  
  
 在上述查询中，只有查询 4 立即执行。  这是因为它返回单个值，而不是一个泛型 <xref:System.Collections.Generic.IEnumerable%601> 集合。  方法本身必须使用 `foreach` 才能计算它的值。  
  
 上述每个查询都可以通过结合使用隐式类型化与 [var](../../../csharp/language-reference/keywords/var.md) 进行编写，如下面的示例所示：  
  
 [!code-cs[csProgGuideLINQ#8](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_4.cs)]  
  
## 示例  
  
## 混合的查询和方法语法  
 此示例演示如何对查询子句的结果使用方法语法。  只需将查询表达式括在括号内，然后应用点运算符并调用此方法。  在下面的示例中，查询 7 返回其值在 3 和 7 之间的数字个数。  但是，通常更好的做法是使用另一个变量来存储方法调用的结果。  这样就不太容易将查询本身与查询结果相混淆。  
  
 [!code-cs[csProgGuideLINQ#9](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-write-linq-queries_5.cs)]  
  
 由于查询 7 返回单个值而不是一个集合，因此该查询立即执行。  
  
 上述查询可以通过结合使用隐式类型化与 `var` 进行编写，如下所示：  
  
```  
var numCount = (from num in numbers...  
```  
  
 它可以按如下方式使用方法语法进行编写：  
  
```  
var numCount = numbers.Where(n => n < 3 || n > 7).Count();  
```  
  
 它可以按如下方式使用显式类型化进行编写：  
  
```  
int numCount = numbers.Where(n => n < 3 || n > 7).Count();  
```  
  
## 请参阅  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Walkthrough: Writing Queries in C\#](../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)   
 [where 子句](../../../csharp/language-reference/keywords/where-clause.md)