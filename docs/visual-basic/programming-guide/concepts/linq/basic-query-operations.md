---
title: "基本查询操作 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据源 [Visual Basic 中的 LINQ]"
  - "Join 子句 [Visual Basic 中的 LINQ]"
  - "对数据进行排序 [Visual Basic 中的 LINQ]"
  - "投影 [Visual Basic 中的 LINQ]"
  - "LINQ [Visual Basic], 查询操作"
  - "Order By 子句 [Visual Basic 中的 LINQ]"
  - "联接数据 [Visual Basic 中的 LINQ]"
  - "查询 [Visual Basic 中的 LINQ], 基本操作"
  - "选择数据 [Visual Basic 中的 LINQ]"
  - "Group By 子句 [Visual Basic 中的 LINQ]"
  - "数据分组 [Visual Basic 中的 LINQ]"
  - "Select 子句 [Visual Basic 中的 LINQ]"
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
caps.latest.revision: 37
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 35
---
# 基本查询操作 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本主题简要介绍 Visual Basic 中的[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext-md.md)] 表达式，以及您在查询中执行的一些典型类型的运算。  有关更多信息，请参见下列主题：  
  
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)  
  
 [查询](../../../../visual-basic/language-reference/queries/queries.md)  
  
 [演练：用 Visual Basic 编写查询](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)  
  
## 指定数据源 \(From\)  
 在 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询中，第一步是指定要查询的数据源。  因此，查询中的 `From` 子句总是最先出现。查询运算符选择、用于根据源的类型的结果。  
  
 [!code-vb[VbLINQBasicOps#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_1.vb)]  
  
 `From` 子句指定数据源 `customers` 和范围变量 `cust`。  范围变量类似于循环迭代变量，但在查询表达式中，实际上不发生迭代。  执行查询（通常使用 `For Each` 循环执行）时，范围变量将用作对 `customers` 中的每个后续元素的引用。  因为编译器可以推断 `cust` 的类型，所以您不必显式指定此类型。  有关使用和不使用显式指定的类型编写的查询示例，请参见[Type Relationships in Query Operations \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md)。  
  
 有关如何在 Visual Basic 中使用 `From` 子句的更多信息，请参见 [From 子句](../../../../visual-basic/language-reference/queries/from-clause.md)。  
  
## 筛选数据 \(Where\)  
 也许最常用的查询操作是应用布尔表达式形式的筛选器。  因此，这种查询只返回那些表达式结果为 true 的元素。  `Where` 子句用于执行筛选。  筛选器指定要在结果序列中包含数据源中的哪些元素。  在下面的示例中，只包含那些地址位于伦敦的客户。  
  
 [!code-vb[VbLINQBasicOps#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_2.vb)]  
  
 您可以使用逻辑运算符（如 `And` 和 `Or`）将筛选器表达式组合在 `Where` 子句中。  例如，若要只返回位于伦敦并且姓名为 Devon 的客户，请使用下面的代码：  
  
```vb#  
Where cust.City = "London" And cust.Name = "Devon"   
```  
  
 若要返回位于伦敦或巴黎的客户，请使用下面的代码：  
  
```vb#  
Where cust.City = "London" Or cust.City = "Paris"   
```  
  
 有关如何在 Visual Basic 中使用 `Where` 子句的更多信息，请参见 [Where 子句](../../../../visual-basic/language-reference/queries/where-clause.md)。  
  
## 对数据进行排序 \(Order By\)  
 将返回的数据按特定的顺序排列通常会带来方便。  `Order By` 子句将使所返回序列中的元素按指定的一个或多个字段排序。  例如，下面的查询基于 `Name` 属性对结果排序。  由于 `Name` 是一个字符串，因此返回的数据将按字母 A 到 Z 的顺序排序。  
  
 [!code-vb[VbLINQBasicOps#3](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_3.vb)]  
  
 若要按相反顺序（从 Z 到 A）对结果排序，请使用 `Order By...Descending` 子句。  如果 `Ascending` 和 `Descending` 都未指定，则默认为 `Ascending`。  
  
 有关如何在 Visual Basic 中使用 `Order By` 子句的更多信息，请参见 [Order By 子句](../../../../visual-basic/language-reference/queries/order-by-clause.md)。  
  
## 选择数据 \(Select\)  
 `Select` 子句指定所返回元素的形式和内容。  例如，您可以指定结果包含的是整个 `Customer` 对象、仅一个 `Customer` 属性、属性的子集、来自不同数据源的属性的组合，还是一些基于计算的新结果类型。  当 `Select` 子句生成除源元素副本以外的内容时，该操作称为“投影”。  
  
 若要检索包含整个 `Customer` 对象的集合，请选择范围变量本身：  
  
 [!code-vb[VbLINQBasicOps#4](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_4.vb)]  
  
 如果 `Customer` 实例是一个包含许多字段的大型对象，而您要检索的只是名称，则可以选择 `cust.Name`，如下面的示例所示。  局部类型推理知道此操作会将结果类型从 `Customer` 对象集合更改为字符串集合。  
  
 [!code-vb[VbLINQBasicOps#5](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_5.vb)]  
  
 若要从数据源中选择多个字段，您可以使用两种方法：  
  
-   在 `Select` 子句中，指定要包含在结果中的字段。  编译器将定义一个匿名类型，该类型将这些字段作为其属性。  有关更多信息，请参见[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
     由于下面示例中的返回元素是匿名类型的实例，因此您无法在代码中的其他位置按名称引用该类型。  编译器为该类型指定的名称含有在普通 Visual Basic 代码中无效的字符。  在下面的示例中，`londonCusts4` 内的查询返回的集合中的元素是某个匿名类型的实例  
  
     [!code-vb[VbLINQBasicOps#6](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_6.vb)]  
  
     \- 或 \-  
  
-   定义含有您要包括在结果中的特定字段的命名类型，并在 `Select` 子句中创建和初始化该类型的实例。  仅当您必须在返回各个结果的集合以外使用这些结果，或者必须将这些结果作为参数传入方法调用时，才使用此选项。  下面的示例中的 `londonCusts5` 类型是 IEnumerable\(Of NamePhone\)。  
  
     [!code-vb[VbLINQBasicOps#7](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_7.vb)]  
  
     [!code-vb[VbLINQBasicOps#8](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_8.vb)]  
  
 有关如何在 Visual Basic 中使用 `Select` 子句的更多信息，请参见 [Select 子句](../../../../visual-basic/language-reference/queries/select-clause.md)。  
  
## 联接数据（Join 和 Group Join）  
 您可以使用多种方法将多个数据源组合到 `From` 子句中。  例如，下面的代码使用两个数据源并将来自这二者的属性隐式组合在结果中。  该查询选择姓氏以元音开头的学生。  
  
 [!code-vb[VbLINQBasicOps#9](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_9.vb)]  
  
> [!NOTE]
>  您可以使用[How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)中创建的学生列表运行此代码。  
  
 `Join` 关键字等效于 SQL 中的 `INNER JOIN`。  它基于两个集合中的元素之间的匹配键值对这两个集合进行组合。  该查询返回包含这些匹配键值的全部或部分集合元素。  例如，下面的代码复制上面的隐式联接操作。  
  
 [!code-vb[VbLINQBasicOps#10](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_10.vb)]  
  
 `Group Join` 将多个集合组合为单个分层集合，就像 SQL 中的 `LEFT JOIN`。  有关更多信息，请参见[Join 子句](../../../../visual-basic/language-reference/queries/join-clause.md)和[Group Join 子句](../../../../visual-basic/language-reference/queries/group-join-clause.md)。  
  
## 对数据进行分组 \(Group By\)  
 您可以添加 `Group By` 子句，以根据元素的一个或多个字段对查询结果中的元素进行分组。  例如，下面的代码按年级 \(class year\) 对学生进行分组。  
  
 [!code-vb[VbLINQBasicOps#11](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_11.vb)]  
  
 如果您使用[How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)中创建的学生列表运行此代码，则 `For Each` 语句将输出：  
  
 Year: Junior  
  
 Tucker, Michael  
  
 Garcia, Hugo  
  
 Garcia, Debra  
  
 Tucker, Lance  
  
 Year: Senior  
  
 Omelchenko, Svetlana  
  
 Osada, Michiko  
  
 Fakhouri, Fadi  
  
 Feng, Hanying  
  
 Adams, Terry  
  
 Year: Freshman  
  
 Mortensen, Sven  
  
 Garcia, Cesar  
  
 下面显示的代码变体对年级排序，然后对每个年级的学生按姓氏排序。  
  
 [!code-vb[VbLINQBasicOps#12](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/visualbasic/basic-query-operations_12.vb)]  
  
 有关`Group By`的更多信息，请参见[Group By 子句](../../../../visual-basic/language-reference/queries/group-by-clause.md)。  
  
## 请参阅  
 <xref:System.Collections.Generic.IEnumerable%601>   
 [Getting Started with LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Basic LINQ Query Operations](../../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)