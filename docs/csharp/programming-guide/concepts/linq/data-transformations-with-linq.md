---
title: "使用 LINQ 进行数据转换 (C#) | Microsoft Docs"
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
  - "LINQ [C#]，数据转换"
  - "源元素 [C# 中的 LINQ]"
  - "联接多个输入 [C# 中的 LINQ]"
  - "一个输出序列的多个输出 [C# 中的 LINQ]"
  - "源元素的子集 [C# 中的 LINQ]"
  - "数据源 [C# 中的 LINQ]，数据转换"
  - "数据转换 [C# 中的 LINQ]"
ms.assetid: 674eae9e-bc72-4a88-aed3-802b45b25811
caps.latest.revision: 17
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 使用 LINQ 进行数据转换 (C#)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbteclinqext](../../../../csharp/programming-guide/concepts/linq/includes/vbteclinqext_md.md)] 不仅可用于检索数据，  而且还是一个功能强大的数据转换工具。  通过使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询，您可以将源序列用作输入，并采用多种方式修改它以创建新输出序列。  您可以修改该序列，而不必修改元素通过排序和分组。本身。但是，[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询的最强大功能是能够创建新类型。  这一功能在 [select](../../../../csharp/language-reference/keywords/select-clause.md) 子句中实现。  例如，可以执行下列任务：  
  
-   将多个输入序列合并到具有新类型的单个输出序列中。  
  
-   创建其元素只包含源序列中的各个元素的一个或几个属性的输出序列。  
  
-   创建其元素包含对源数据执行的操作结果的输出序列。  
  
-   创建不同格式的输出序列。  例如，您可以将 SQL 行或文本文件的数据转换为 XML。  
  
 这只是几个示例。  当然，可以采用多种方式将这些转换组合在同一查询中。  另外，一个查询的输出序列可用作新查询的输入序列。  
  
## 将多个输入联接到一个输出序列  
 可以使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询来创建包含多个输入序列的元素的输出序列。  下面的示例演示如何组合两个内存中的数据结构，但组合来自 XML 或 SQL 或数据集源的数据时可应用相同的原则。  假定下面两种类类型：  
  
 [!code-cs[CsLINQGettingStarted#7](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_1.cs)]  
  
 下面的示例演示该查询：  
  
 [!code-cs[CSLinqGettingStarted#8](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_2.cs)]  
  
 有关更多信息，请参见[join 子句](../../../../csharp/language-reference/keywords/join-clause.md)和[select 子句](../../../../csharp/language-reference/keywords/select-clause.md)。  
  
## 选择各个源元素的子集  
 选择源序列中的各个元素的子集有两种主要方法：  
  
1.  若要只选择源元素的一个成员，请使用点运算。  在下面的示例中，假定 `Customer` 对象包含几个公共属性，其中包括名为 `City` 的字符串。  在执行此查询时，此查询将生成字符串输出序列。  
  
    ```  
    var query = from cust in Customers  
                select cust.City;  
    ```  
  
2.  若要创建包含源元素的多个属性的元素，可以使用具有命名对象或匿名类型的对象初始值设定项。  下面的示例演示如何使用匿名类型来封装各个 `Customer` 元素的两个属性：  
  
    ```  
    var query = from cust in Customer  
                select new {Name = cust.Name, City = cust.City};  
    ```  
  
 有关更多信息，请参见[对象和集合初始值设定项](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)和[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
## 将内存中的对象转换为 XML  
 通过 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询，可以轻松地在内存中的数据结构、SQL 数据库、[!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] 数据集和 XML 流或文档之间转换数据。  下面的示例将内存中的数据结构中的对象转换为 XML 元素。  
  
 [!code-cs[CsLINQGettingStarted#9](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_3.cs)]  
  
 此代码生成下面的 XML 输出：  
  
```  
< Root>  
  <student>  
    <First>Svetlana</First>  
    <Last>Omelchenko</Last>  
    <Scores>97,92,81,60</Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell</Last>  
    <Scores>75,84,91,39</Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen</Last>  
    <Scores>88,94,65,91</Scores>  
  </student>  
</Root>  
```  
  
 有关更多信息，请参见[使用 C\# 创建 XML 树](../Topic/Creating%20XML%20Trees%20in%20C%23%20\(LINQ%20to%20XML\)1.md)。  
  
## 对源元素执行操作  
 输出序列可能不包含源序列的任何元素或元素属性。  输出可能是通过将源元素用作输入参数计算出的值的序列。  在执行下面这个简单查询时，此查询会输出一个字符串序列，该序列值表示根据 `double` 类型的元素的源序列进行的计算。  
  
> [!NOTE]
>  如果查询将转换为某个其他域，则不支持在查询表达式中调用方法。  例如，不能在 [!INCLUDE[vbtecdlinq](../../../../csharp/language-reference/keywords/includes/vbtecdlinq_md.md)] 中调用一般 C\# 方法，因为 SQL Server 没有该方法的上下文。  但是，可以将存储过程映射到方法，然后调用方法。  有关更多信息，请参见[存储过程](../Topic/Stored%20Procedures.md)。  
  
 [!code-cs[CsLINQGettingStarted#10](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/data-transformations-with-linq_4.cs)]  
  
## 请参阅  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md)   
 [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)   
 [LINQ 查询表达式](../../../../visual-basic/reference/command-line-compiler/index.md)   
 [select 子句](../../../../csharp/language-reference/keywords/select-clause.md)   
 [如何：使用联接合并数据](../../../../visual-basic/programming-guide/language-features/linq/how-to-combine-data-with-linq-by-using-joins.md)