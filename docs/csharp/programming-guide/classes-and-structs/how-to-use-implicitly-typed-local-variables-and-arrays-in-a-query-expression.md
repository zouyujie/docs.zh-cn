---
title: "如何：在查询表达式中使用隐式类型的局部变量和数组（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "隐式类型的局部变量 [C#], 使用方法"
ms.assetid: 6b7354d2-af79-427a-b6a8-f74eb8fd0b91
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# 如何：在查询表达式中使用隐式类型的局部变量和数组（C# 编程指南）
如果希望用编译器来确定局部变量的类型，则可以使用隐式类型化局部变量。  必须使用隐式类型化局部变量来存储匿名类型，后者通常用于查询表达式。  以下示例演示查询中可选择使用以及必须使用的隐式类型化局部变量。  
  
 隐式类型化局部变量是使用 [var](../../../csharp/language-reference/keywords/var.md) 上下文关键字声明的。  有关更多信息，请参见[隐式类型的局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)和[隐式类型的数组](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)。  
  
## 示例  
 下面的示例显示了需要 `var` 关键字的常见方案：即产生匿名类型序列的查询表达式。  在此方案中，因为您无权访问匿名类型的类型名称，所以必须使用 `var` 隐式类型化 `foreach` 语句中的查询变量和迭代变量。  有关匿名类型的更多信息，请参见[匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)。  
  
 [!code-cs[csProgGuideLINQ#32](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#32)]  
  
## 示例  
 虽然下面的示例在类似的情况中使用了关键字 `var`，但其中对 `var` 的使用是可选的。  因为 `student.LastName` 是一个字符串，所以执行查询会返回一个字符串序列。  因此，可将 `queryID` 的类型声明为 `System.Collections.Generic.IEnumerable<string>`，而不是 `var`。  为方便起见，可使用关键字 `var`。  在该示例中，`foreach` 语句中的迭代变量被显式类型化为一个字符串，但它也可改用 `var` 声明。  由于迭代变量的类型不是匿名类型，因此，可选择（而不强制要求）使用 `var`。  请记住，`var` 本身不是类型，而是一条指示编译器推断和分配类型的指令。  
  
 [!code-cs[csProgGuideLINQ#33](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#33)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [扩展方法](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [var](../../../csharp/language-reference/keywords/var.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)