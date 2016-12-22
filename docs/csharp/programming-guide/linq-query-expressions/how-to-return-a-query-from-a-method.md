---
title: "如何：从方法中返回查询（C# 编程指南） | Microsoft Docs"
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
  - "方法返回查询 [C#]"
  - "查询 [C# 中的 LINQ], 方法返回查询"
  - "查询表达式 [C# 中的 LINQ], 方法返回查询"
ms.assetid: 9d6f20a7-f085-44cf-9df3-71948255ec68
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：从方法中返回查询（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

此示例演示如何从某一方法以返回值和 `out` 参数的形式返回查询。  
  
 任何查询的类型都必须为 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601>，或一种派生类型（如 <xref:System.Linq.IQueryable%601>）。  因此，返回查询的方法的任何返回值或 `out` 参数也必须具有该类型。  如果某个方法将查询具体化为具体的 <xref:System.Collections.Generic.List%601> 或 <xref:System.Array> 类型，则认为该方法在返回查询结果（而不是查询本身）。  仍然能够编写或修改从方法返回的查询变量。  
  
## 示例  
 在下面的示例中，第一个方法以返回值的形式返回查询，第二个方法以 `out` 参数的形式返回查询。  请注意，在这两种情况下，返回的都是查询，而不是查询结果。  
  
 [!code-cs[csProgGuideLINQ#80](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-return-a-query-from-a-method_1.cs)]  
  
## 编译代码  
  
-   创建面向 .NET Framework 3.5 或更高版本的 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] 项目。  默认情况下，该项目具有一个对 System.Core.dll 的引用以及一条针对 System.Linq 命名空间的 `using` 指令。  
  
-   将类替换为示例中的代码。  
  
-   按 F5 编译并运行程序。  
  
-   按任意键退出控制台窗口。  
  
## 请参阅  
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)