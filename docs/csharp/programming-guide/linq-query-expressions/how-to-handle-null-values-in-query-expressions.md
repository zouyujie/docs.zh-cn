---
title: "如何：在查询表达式中处理 Null 值（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "null 值 [C# 中的 LINQ]"
  - "查询 [C# 中的 LINQ], null 值"
  - "查询表达式 [C# 中的 LINQ], null 值"
ms.assetid: cb34f7a1-7ef5-466a-90ba-91da30ab525d
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在查询表达式中处理 Null 值（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

此示例演示如何处理源集合中可能的 null 值。  诸如 <xref:System.Collections.Generic.IEnumerable%601> 等对象集合可能包含值为 [null](../../../csharp/language-reference/keywords/null.md) 的元素。  如果源集合为 null 或包含值为 null 的元素，并且查询未处理 null 值，当您执行查询时将会引发 <xref:System.NullReferenceException>。  
  
## 示例  
 您可以采用防御方式进行编码以避免 null 引用异常，如下面的示例中所示：  
  
 [!code-cs[csProgGuideLINQ#82](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-null-values-in-query-expressions_1.cs)]  
  
 在前面的示例中，`where` 子句筛选出类别序列中的所有 null 元素。  此技术与 join 子句中的 null 检查无关。  此示例中包含 null 的条件表达式将发挥作用，因为 `Products.CategoryID` 的类型为 `int?`（`Nullable<int>` 的简写形式）。  
  
## 示例  
 在 join 子句中，只要其中一个比较键是可以为 null 的类型，您就可以在查询表达式中将另一个比较键强制转换成可以为 null 的类型。  在下面的示例中，假定 `EmployeeID` 是一个列，其中包含类型为 `int?` 的值：  
  
 [!code-cs[csProgGuideLINQ#83](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-null-values-in-query-expressions_2.cs)]  
  
## 请参阅  
 <xref:System.Nullable%601>   
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)   
 [可以为 null 的类型](../../../visual-basic/reference/command-line-compiler/index.md)