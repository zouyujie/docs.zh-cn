---
title: "查询表达式基础（C# 编程指南） | Microsoft Docs"
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
  - "查询 [C# 中的 LINQ], 基本知识"
  - "查询表达式 [C# 中的 LINQ], 基本知识"
  - "查询表达式 [C# 中的 LINQ], 查询执行"
ms.assetid: d3e1f4e6-1cf0-4066-87e3-1a42387223a6
caps.latest.revision: 32
caps.handback.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 查询表达式基础（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## 什么是查询？它有什么用途？  
 “查询”是指一组指令，这些指令描述要从一个或多个给定数据源检索的数据以及返回的数据应该使用的格式和组织形式。  查询不同于它所产生的结果。  
  
 通常，源数据会在逻辑上组织为相同种类的元素序列。  SQL 数据库表包含一个行序列。  与此类似，[!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] <xref:System.Data.DataTable> 包含一个 <xref:System.Data.DataRow> 对象序列。  在 XML 文件中，有一个 XML 元素“序列”（不过这些元素按分层形式组织为树结构）。  内存中的集合包含一个对象序列。  
  
 从应用程序的角度来看，原始源数据的具体类型和结构并不重要。  应用程序始终将源数据视为一个 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Linq.IQueryable%601> 集合。  在 [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中，源数据显示为一个 `IEnumerable`\<<xref:System.Xml.Linq.XElement>\>。  在 [!INCLUDE[linq_dataset](../../../csharp/programming-guide/linq-query-expressions/includes/linq_dataset_md.md)] 中，它是一个 `IEnumerable`\<<xref:System.Data.DataRow>\>。  在 [!INCLUDE[vbtecdlinq](../../../csharp/language-reference/keywords/includes/vbtecdlinq_md.md)] 中，它是您定义用来表示 SQL 表中数据的任何自定义对象的 `IEnumerable` 或 `IQueryable`。  
  
 指定此源序列后，查询可以进行下列三项工作之一：  
  
-   检索一个元素子集以产生一个新序列，但不修改单个元素。  然后，查询可以按各种方式对返回的序列进行排序或分组，如下面的示例所示（假定 `scores` 是 `int[]`）：  
  
     [!code-cs[csrefQueryExpBasics#45](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_1.cs)]  
  
-   如上一个示例所述检索一个元素序列，但是将这些元素转换为具有新类型的对象。  例如，查询可以只从数据源中的某些客户记录检索姓氏。  或者，查询可以检索完整的记录，再使用它构建另一个内存中对象类型甚至 XML 数据，然后生成最终的结果序列。  下面的示例演示了从 `int` 到 `string` 的转换。  请注意 `highScoresQuery` 的新类型。  
  
     [!code-cs[csrefQueryExpBasics#46](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_2.cs)]  
  
-   检索有关源数据的单一值，例如：  
  
    -   符合某个条件的元素的数量。  
  
    -   具有最大值或最小值的元素。  
  
    -   符合某个条件的第一个元素，或一组指定元素中的特定值之和。  例如，下面的查询从 `scores` 整数数组中返回高于 80 的分数的数量。  
  
     [!code-cs[csrefQueryExpBasics#47](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_3.cs)]  
  
     在上一个示例中，请注意在 `Count` 方法调用之前的查询表达式两旁使用了括号。  另一种表示方式是使用一个新变量来存储具体结果。  此技术的可读性更好，因为它将存储查询的变量与存储结果的查询区分开来。  
  
     [!code-cs[csrefQueryExpBasics#48](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_4.cs)]  
  
 在上一个示例中，查询是在 `Count` 调用中执行的，因为 `Count` 必须循环访问结果以便确定 `highScoresQuery` 返回的元素数量。  
  
## 什么是查询表达式？  
 “查询表达式”是用查询语法表示的查询，  是一流的语言构造。  它就像任何其他表达式一样，并且可以用在 C\# 表达式有效的任何上下文中。  查询表达式由一组用类似于 SQL 或 XQuery 的声明性语法编写的子句组成。  每个子句又包含一个或多个 C\# 表达式，而这些表达式本身又可能是查询表达式或包含查询表达式。  
  
 查询表达式必须以 [from](../../../csharp/language-reference/keywords/from-clause.md) 子句开头，并且必须以 [select](../../../csharp/language-reference/keywords/select-clause.md) 或 [group](../../../csharp/language-reference/keywords/group-clause.md) 子句结尾。  在第一个 `from` 子句和最后一个 `select` 或 `group` 子句之间，查询表达式可以包含一个或多个下列可选子句：[where](../../../csharp/language-reference/keywords/where-clause.md)、[orderby](../../../csharp/language-reference/keywords/orderby-clause.md)、[join](../../../csharp/language-reference/keywords/join-clause.md)、[let](../../../csharp/language-reference/keywords/let-clause.md) 甚至附加的 [from](../../../csharp/language-reference/keywords/from-clause.md) 子句。  还可以使用 [into](../../../csharp/language-reference/keywords/into.md) 关键字使 `join` 或 `group` 子句的结果能够充当同一查询表达式中附加查询子句的源。  
  
### 查询变量  
 在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 中，查询变量是任何存储查询（而非查询结果）的变量。更具体地说，查询变量始终是一个可枚举的类型，当在 `foreach` 语句中或在对其 `IEnumerator.MoveNext` 方法的直接调用中循环访问它时，它会生成一序列元素。  
  
 下面的代码示例演示了一个简单的查询表达式，它含有一个数据源、一个筛选子句和一个排序子句，但不对源元素进行转换。  `select` 子句结束了该查询。  
  
 [!code-cs[csrefQueryExpBasics#49](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_5.cs)]  
  
 在上一个示例中，`scoreQuery` 是一个查询变量，有时简称为“查询”。  查询变量并不存储实际的结果数据（这些数据是在 `foreach` 循环中产生的）。  另外，当 `foreach` 语句执行时，查询结果并不是通过查询变量 `scoreQuery` 返回的。  相反，它们是通过迭代变量 `testScore` 返回的。  可以在另一个 `foreach` 循环中迭代 `scoreQuery` 变量。  只要该变量和数据源都没有修改，该变量都将产生相同的结果。  
  
 查询变量可以存储用查询语法或方法语法（或二者的组合）表示的查询。  在下面的示例中，`queryMajorCities` 和 `queryMajorCities2` 都是查询变量：  
  
 [!code-cs[csrefQueryExpBasics#50](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_6.cs)]  
  
 另一方面，下面的两个示例演示了不是查询变量的变量，即使每个变量都用查询进行了初始化。  它们不是查询变量的原因是它们存储了结果：  
  
 [!code-cs[csrefQueryExpBasics#51](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_7.cs)]  
  
> [!NOTE]
>  在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 文档中，存储查询的变量在其名称中包含单词“query”，  而存储实际结果的变量在其名称中不包含单词“query”。  
  
 有关用于表示查询的不同方式的更多信息，请参见[Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)。  
  
#### 查询变量的显式类型化和隐式类型化  
 本文档通常提供查询变量的显式类型，以便演示查询变量和 [select 子句](../../../csharp/language-reference/keywords/select-clause.md)之间的类型关系。  但是，也可以使用 [var](../../../csharp/language-reference/keywords/var.md) 关键字指示编译器在编译时推断查询变量（或任何其他本地变量）的类型。  例如，还可以使用隐式类型化表示本主题前面部分中演示的查询示例：  
  
 [!code-cs[csrefQueryExpBasics#52](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_8.cs)]  
  
 有关更多信息，请参见[隐式类型的局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)和 [Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)。  
  
### 开始查询表达式  
 查询表达式必须以 `from` 子句开头。  它同时指定了数据源和范围变量。  在对源序列进行遍历的过程中，范围变量表示源序列中的每个后续元素。  将根据数据源中元素的类型对范围变量进行强类型化。  在下面的示例中，因为 `countries` 是 `Country` 对象数组，所以范围变量也被类型化为 `Country`，  这样就可以使用点运算符来访问该类型的任何可用成员。  
  
 [!code-cs[csrefQueryExpBasics#53](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_9.cs)]  
  
 在使用分号或延续子句退出查询之前，范围变量将一直位于范围中。  
  
 查询表达式可以包含多个 `from` 子句。  当源序列中的每个元素本身就是集合或包含集合时，可使用附加的 `from` 子句。  例如，假定您具有一个 `Country` 对象集合，而其中每个对象都包含一个名为 `Cities` 的 `City` 对象集合。  若要查询每个 `Country` 中的 `City` 对象，请使用两个`from` 子句，如下所示：  
  
 [!code-cs[csrefQueryExpBasics#54](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_10.cs)]  
  
 有关更多信息，请参见 [from 子句](../../../csharp/language-reference/keywords/from-clause.md)。  
  
### 结束查询表达式  
 查询表达式必须以 `select` 子句或 `group` 子句结尾。  
  
#### group 子句  
 使用 `group` 子句可产生按照指定的键组织的组序列。  键可以采用任何数据类型。  例如，下面的查询创建一个组序列，该序列包含一个或多个 `Country` 对象，并且它的键是 `char` 值。  
  
 [!code-cs[csrefQueryExpBasics#55](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_11.cs)]  
  
 有关分组的更多信息，请参见 [group 子句](../../../csharp/language-reference/keywords/group-clause.md)。  
  
#### select 子句  
 使用 `select` 子句可产生所有其他类型的序列。  简单的 `select` 子句只是产生与数据源中包含的对象具有相同类型的对象的序列。  在此示例中，数据源包含 `Country` 对象。  `orderby` 子句只是将元素重新排序，而 `select` 子句则产生重新排序的 `Country` 对象的序列。  
  
 [!code-cs[csrefQueryExpBasics#56](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_12.cs)]  
  
 可以使用 `select` 子句将源数据转换为新类型的序列。  这一转换也称为“投影”。  在下面的示例中，`select` 子句对一个匿名类型序列进行投影，该序列仅包含原始元素中各字段的子集。  请注意，新对象是使用对象初始值设定项初始化的。  
  
 [!code-cs[csrefQueryExpBasics#57](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_13.cs)]  
  
 有关使用 `select` 子句转换源数据的所有方式的更多信息，请参见 [select 子句](../../../csharp/language-reference/keywords/select-clause.md)。  
  
#### 使用“into”进行延续  
 可以在 `select` 或 `group` 子句中使用 `into` 关键字来创建用于存储查询的临时标识符。  当您必须在分组或选择操作之后对查询执行附加查询操作时，需要这样做。  在下面的示例中，以一千万人口范围为界对 `countries` 进行分组。  在创建这些组之后，使用附加子句筛选掉某些组，然后按升序对剩下的组进行排序。  若要执行这些附加操作，需要使用由 `countryGroup` 表示的延续。  
  
 [!code-cs[csrefQueryExpBasics#58](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_14.cs)]  
  
 有关更多信息，请参见 [into](../../../csharp/language-reference/keywords/into.md)。  
  
### 筛选、排序和联接  
 在 `from` 开始子句以及 `select` 或 `group` 结束子句之间，所有其他子句（`where`、`join`、`orderby`、`from`、`let`）都是可选的。  任何可选子句都可以在查询正文中使用零次或多次。  
  
#### where 子句  
 使用 `where` 子句可以根据一个或多个谓词表达式筛选掉源数据中的某些元素。  以下示例中的 `where` 子句含有两个谓词。  
  
 [!code-cs[csrefQueryExpBasics#59](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_15.cs)]  
  
 有关更多信息，请参见 [where 子句](../../../csharp/language-reference/keywords/where-clause.md)。  
  
#### orderby 子句  
 使用 `orderby` 子句可以按升序或降序对结果进行排序。  您还可以指定次要排序顺序。  下面的示例使用 `Area` 属性对 `country` 对象执行主要排序，  然后使用 `Population` 属性执行次要排序。  
  
 [!code-cs[csrefQueryExpBasics#60](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_16.cs)]  
  
 `ascending` 关键字是可选的；如果未指定顺序，则它是默认排序顺序。  有关更多信息，请参见 [orderby 子句](../../../csharp/language-reference/keywords/orderby-clause.md)。  
  
#### join 子句  
 使用 `join` 子句可以根据每个元素中指定键之间的相等比较，对一个数据源中的元素与另外一个数据源中的元素进行关联和\/或组合。  在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 中，联接操作是针对其元素具有不同类型的对象序列执行的。  在联接两个序列之后，必须使用 `select` 或 `group` 语句指定要存储到输出序列中的元素。  还可以使用匿名类型将每组关联元素中的属性组合为输出序列的新类型。  下面的示例对其 `Category` 属性与 `categories` 字符串数组中的某个类别相匹配的 `prod` 对象进行关联。  其 `Category` 不与 `categories` 中的任何字符串匹配的产品会被筛选掉。  `select` 语句投影了一个新类型，其属性取自 `cat` 和 `prod`。  
  
 [!code-cs[csrefQueryExpBasics#61](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_17.cs)]  
  
 通过使用 [into](../../../csharp/language-reference/keywords/into.md) 关键字将 `join` 操作的结果存储到临时变量中，还可以执行分组联接。  有关更多信息，请参见 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)。  
  
#### let 子句  
 使用 `let` 子句可以将表达式（如方法调用）的结果存储到新的范围变量中。  在下面的示例中，范围变量 `firstName` 存储了 `Split` 返回的字符串数组的第一个元素。  
  
 [!code-cs[csrefQueryExpBasics#62](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_18.cs)]  
  
 有关更多信息，请参见 [let 子句](../../../csharp/language-reference/keywords/let-clause.md)。  
  
### 查询表达式中的子查询  
 查询子句本身可能包含一个查询表达式，该查询表达式有时称为“子查询”。  每个子查询都以它自己的 `from` 子句开头，该子句不一定指向第一个 `from` 子句中的同一数据源。  例如，下面的查询演示了一个在 select 语句中使用的查询表达式，用来检索分组操作的结果。  
  
 [!code-cs[csrefQueryExpBasics#63](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/query-expression-basics_19.cs)]  
  
 有关更多信息，请参见 [如何：对分组操作执行子查询](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)