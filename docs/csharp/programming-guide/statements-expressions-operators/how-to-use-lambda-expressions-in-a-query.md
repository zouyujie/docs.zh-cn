---
title: "如何：在查询中使用 Lambda 表达式（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "lambda 表达式 [C#], 在 LINQ 中"
ms.assetid: 3cac4d25-d11f-4abd-9e7c-0f02e97ae06d
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在查询中使用 Lambda 表达式（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

您不会在查询语法中直接用到 Lambda 表达式，但会在方法调用中用到这些表达式，并且查询表达式可以包含方法调用。  事实上，某些查询操作只能用方法语法表示。  有关查询语法和方法语法之间的区别的更多信息，请参见[Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)。  
  
## 示例  
 下面的示例演示如何通过使用 <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName> 标准查询运算符在基于方法的查询中使用 Lambda 表达式。  请注意，此示例中的 <xref:System.Linq.Enumerable.Where%2A> 方法具有一个委托类型为 <xref:System.Func%601> 的输入参数，并且委托采用整数作为输入并返回布尔值。  可以将 Lambda 表达式转换为该委托。  假若这是使用 <xref:System.Linq.Queryable.Where%2A?displayProperty=fullName> 方法的 [!INCLUDE[vbtecdlinq](../../../csharp/language-reference/keywords/includes/vbtecdlinq_md.md)] 查询，则参数类型将为 `Expression<Func\<int,bool>>`，但 Lambda 表达式看起来将完全相同。  有关表达式类型的更多信息，请参见 <xref:System.Linq.Expressions.Expression?displayProperty=fullName>。  
  
 [!code-cs[csProgGuideLINQ#1](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-use-lambda-expressions-in-a-query_1.cs)]  
  
## 示例  
 下面的示例演示如何在查询表达式的方法调用中使用 Lambda 表达式。  Lambda 是必需的，因为无法使用查询语法来调用 <xref:System.Linq.Enumerable.Sum%2A> 标准查询运算符。  
  
 查询首先按 `GradeLevel` 枚举中定义的方式，依据学生的成绩等级对学生进行分组。  然后，对于每个组，查询将添加每名学生的总分。  这需要两个 `Sum` 运算。  内部的 `Sum` 计算每名学生的总分，外部的 `Sum` 保留该组中所有学生的运行合并总计。  
  
 [!code-cs[csProgGuideLINQ#2](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-use-lambda-expressions-in-a-query_2.cs)]  
  
## 编译代码  
 若要运行此代码，请将方法复制并粘贴到[如何：查询对象集合](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md)中提供的 `StudentClass` 中，并从 `Main` 方法中调用它。  
  
## 请参阅  
 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [表达式树](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)