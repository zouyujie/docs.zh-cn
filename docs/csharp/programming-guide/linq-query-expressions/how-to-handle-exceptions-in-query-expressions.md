---
title: "如何：在查询表达式中处理异常（C# 编程指南） | Microsoft Docs"
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
  - "异常 [C#], LINQ 查询"
  - "查询 [C# 中的 LINQ], 异常"
  - "查询表达式 [C# 中的 LINQ], 异常"
ms.assetid: 4ce6c081-7731-4b8f-b4fa-d947f165a18a
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在查询表达式中处理异常（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以在查询表达式的上下文中调用任何方法。  但是，建议您避免在查询表达式中调用任何可能产生副作用（例如，修改数据源的内容或引发异常）的方法。  此示例演示在查询表达式中调用方法时如何避免引发异常，同时又不违反 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 的有关异常处理的一般性准则。  这些准则说明：如果您了解为什么在给定上下文中会引发特定异常，那么就可以捕捉该异常。  有关更多信息，请参见[异常的最佳做法](../Topic/Best%20Practices%20for%20Exceptions.md)。  
  
 最后一个示例演示如何处理那些必须在查询执行过程中引发异常的情况。  
  
## 示例  
 下面的示例演示如何将异常处理代码移至查询表达式外部。  仅当该方法不依赖于查询的任何本地变量时，才能这样做。  
  
 [!code-cs[csProgGuideLINQ#10](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-exceptions-in-query-expressions_1.cs)]  
  
## 示例  
 在某些情况下，对在查询内引发的异常的最佳响应可能是立即停止执行查询。  下面的示例演示如何处理可能从查询正文内部引发的异常。  假定 `SomeMethodThatMightThrow` 可能导致要求停止执行查询的异常。  
  
 请注意，`try` 块将 `foreach` 循环而不是查询本身封闭起来。  这是因为 `foreach` 循环是实际执行查询的场所。  有关更多信息，请参见 [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)。  
  
 [!code-cs[csProgGuideLINQ#12](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-exceptions-in-query-expressions_2.cs)]  
  
## 编译代码  
  
-   创建面向 .NET Framework 3.5 版的 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] 项目。  默认情况下，该项目具有一个对 System.Core.dll 的引用以及一条针对 System.Linq 命名空间的 `using` 指令。  
  
-   将代码复制到项目中。  
  
-   按 F5 编译并运行程序。  
  
 按任意键退出控制台窗口。  
  
## 请参阅  
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)