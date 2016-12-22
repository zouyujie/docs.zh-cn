---
title: "如何：执行自定义联接操作（C# 编程指南） | Microsoft Docs"
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
  - "自定义联接 [C#]"
  - "联接 [C#], 自定义"
  - "查询 [C# 中的 LINQ], 联接"
  - "查询表达式 [C# 中的 LINQ], 联接"
ms.assetid: a05e2ab1-410d-4a1d-8ada-af93539682c9
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：执行自定义联接操作（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

此示例演示如何执行无法使用 `join` 子句执行的联接操作。  在查询表达式中，`join` 子句仅适用于同等联接（这是迄今为止最常见的联接操作类型），并针对同等联接进行了优化。  执行同等联接时，一般总是可以通过使用 `join` 子句获得最佳性能。  
  
 但是，在下面一些情况中，无法使用 `join` 子句：  
  
-   联接是在不等式（非同等联接）上断言的。  
  
-   联接是在多个等式或不等式上断言的。  
  
-   必须在联接操作之前为右侧（内部）序列引入一个临时范围变量。  
  
 若要执行非同等联接，可以使用多个 `from` 子句单独引入每个数据源。  然后，在 `where` 子句中将谓词表达式应用于每个源的范围变量。  该表达式还可以采用方法调用的形式。  
  
> [!NOTE]
>  不要将这种自定义联接操作与使用多个 `from` 子句访问内部集合相混淆。  有关更多信息，请参见 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)。  
  
## 示例  
 下面示例中的第一个方法演示了一个简单的交叉联接。  必须慎用交叉联接，因为它们可能产生非常大的结果集。  但在某些方案中，可以使用它们创建源序列以供运行附加查询。  
  
 第二个方法产生其类别 ID 列在左侧类别列表中的所有产品的序列。  请注意，这种方法使用 `let` 子句和 `Contains` 方法创建了一个临时数组。  还可以在查询前创建该数组并去掉第一个 `from` 子句。  
  
 [!code-cs[csProgGuideLINQ#64](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-perform-custom-join-operations_1.cs)]  
  
## 示例  
 在下面的示例中，查询必须基于匹配键联接两个序列，而对于内部（右侧）序列而言，无法在 join 子句本身之前获取这些键。  如果此联接是使用 `join` 子句执行的，则必须为每个元素调用 `Split` 方法。  使用多个 `from` 子句可使查询避免反复进行方法调用的系统开销。  然而，由于 `join` 进行了优化，因此在此特定情况下，它仍然可能比使用多个 `from` 子句快。  结果会有所不同，主要取决于方法调用的系统开销有多大。  
  
 [!code-cs[csProgGuideLINQ#13](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-perform-custom-join-operations_2.cs)]  
  
## 编译代码  
  
-   创建一个面向 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 3.5 或更高版本的 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] 控制台应用程序项目。  默认情况下，该项目具有一个对 System.Core.dll 的引用以及一条针对 System.Linq 命名空间的 `using` 指令。  
  
-   将 `Program` 类替换为上述示例中的代码。  
  
-   按照 [How to: Join Content from Dissimilar Files \(LINQ\)](../Topic/How%20to:%20Join%20Content%20from%20Dissimilar%20Files%20\(LINQ\).md) 中的指令设置数据文件（scores.csv 和 names.csv）。  
  
-   按 F5 编译并运行程序。  
  
-   按任意键退出控制台窗口。  
  
## 请参阅  
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)   
 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [如何：对 Join 子句的结果进行排序](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)