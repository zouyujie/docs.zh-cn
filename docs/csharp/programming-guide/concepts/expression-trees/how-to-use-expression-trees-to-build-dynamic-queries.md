---
title: "如何：使用表达式树来生成动态查询 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 52cd44dd-a3ec-441e-b93a-4eca388119c7
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7de999848870de80996f308affde088088e32e52
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-expression-trees-to-build-dynamic-queries-c"></a>如何：使用表达式树来生成动态查询 (C#)
在 LINQ 中，表达式树用于表示针对数据源的结构化查询，这些数据源实现 <xref:System.Linq.IQueryable%601>。 例如，LINQ 提供程序实现 <xref:System.Linq.IQueryable%601> 接口，用于查询关系数据存储。 C# 编译器将针对此类数据源的查询编译为代码，该代码在运行时会生成一个表达式树。 然后，查询提供程序可以遍历表达式树数据结构，并将其转换为适合于数据源的查询语言。  
  
 表达式树还可以用在 LINQ 中，用于表示分配给类型为 <xref:System.Linq.Expressions.Expression%601> 的变量的 lambda 表达式。  
  
 本主题描述如何使用表达式树来创建动态 LINQ 查询。 如果在编译时不知道查询的细节，动态查询将十分有用。 例如，应用程序可能会提供一个用户界面，最终用户可以使用该用户界面指定一个或多个谓词来筛选数据。 为了使用 LINQ 进行查询，这种应用程序必须使用表达式树在运行时创建 LINQ 查询。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用表达式树依据 `IQueryable` 数据源构造一个查询，然后执行该查询。 代码将生成一个表达式树来表示以下查询：  
  
 `companies.Where(company => (company.ToLower() == "coho winery" || company.Length > 16)).OrderBy(company => company)`  
  
 <xref:System.Linq.Expressions> 命名空间中的工厂方法用于创建表达式树，这些表达式树表示构成总体查询的表达式。 表示标准查询运算符方法调用的表达式将引用这些方法的 <xref:System.Linq.Queryable> 实现。 最终的表达式树传递到 `IQueryable` 数据源的提供程序的 <xref:System.Linq.IQueryProvider.CreateQuery%60%601%28System.Linq.Expressions.Expression%29> 实现，用于创建类型为 `IQueryable` 的可执行查询。 通过枚举该查询变量获得结果。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 此代码在传递到 `Queryable.Where` 方法的谓词中使用固定数量的表达式。 但是，可以编写一个视用户输入而定来合并可变数量谓词表达式的应用程序。 视用户输入而定，也可以更改在查询中调用的标准查询运算符。  
  
## <a name="compiling-the-code"></a>编译代码  
  
-   创建新的**控制台应用程序**项目。  
  
-   添加对 System.Core.dll 的引用（如果尚未引用）。  
  
-   包括 System.Linq.Expressions 命名空间。  
  
-   从示例中复制代码，并将其粘贴到 `Main` 方法中。  
  
## <a name="see-also"></a>请参阅  
 [表达式树 (C#)](../../../../csharp/programming-guide/concepts/expression-trees/index.md)   
 [如何：执行表达式树 (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)   
 [如何：在运行时动态指定谓词筛选器](../../../../csharp/programming-guide/linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)
