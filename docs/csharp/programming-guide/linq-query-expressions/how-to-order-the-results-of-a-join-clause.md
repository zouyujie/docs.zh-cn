---
title: "如何：对 Join 子句的结果进行排序（C# 编程指南） | Microsoft Docs"
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
  - "join 子句 [C#]"
  - "联接 [C#], 对结果排序"
  - "查询 [C# 中的 LINQ], 联接"
  - "查询表达式 [C# 中的 LINQ], 联接"
ms.assetid: 83f36f16-2ba3-453f-8b9f-7d02b415610e
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：对 Join 子句的结果进行排序（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

此示例演示如何对联接运算的结果进行排序。  请注意，排序是在联接之后执行的。  尽管可以在联接之前将 `orderby` 子句用于一个或多个源序列，但通常我们不建议这样做。  某些 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 提供程序可能不会在联接之后保留排序。  
  
## 示例  
 此查询将创建一个分组联接，然后基于类别元素（仍然在范围中）对组进行排序。  在匿名类型初始值设定项中，子查询将对产品序列中的所有匹配元素进行排序。  
  
 [!code-cs[csProgGuideLINQ#81](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-order-the-results-of-a-join-clause_1.cs)]  
  
## 编译代码  
  
-   创建面向 .NET Framework 3.5 版的 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] 项目。  默认情况下，该项目具有一个对 System.Core.dll 的引用以及一条针对 System.Linq 命名空间的 `using` 指令。  
  
-   将代码复制到项目中。  
  
-   按 F5 编译并运行程序。  
  
-   按任意键退出控制台窗口。  
  
## 请参阅  
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)   
 [orderby 子句](../../../csharp/language-reference/keywords/orderby-clause.md)   
 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)