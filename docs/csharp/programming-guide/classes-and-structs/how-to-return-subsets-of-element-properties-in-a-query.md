---
title: "如何：在查询中返回元素属性的子集（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "匿名类型 [C#], 元素属性的子集"
ms.assetid: fabdf349-f443-4e3f-8368-6c471be1dd7b
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# 如何：在查询中返回元素属性的子集（C# 编程指南）
当下列两个条件都满足时，可在查询表达式中使用匿名类型：  
  
-   您只想返回每个源元素的某些属性。  
  
-   您无需在执行查询的方法的范围之外存储查询结果。  
  
 如果您只想从每个源元素中返回一个属性或字段，则只需在 `select` 子句中使用点运算符。  例如，若要只返回每个 `student` 的 `ID`，可以按如下方式编写 `select` 子句：  
  
```  
select student.ID;  
```  
  
## 示例  
 下面的示例演示如何使用匿名类型只返回每个源元素的符合指定条件的属性子集。  
  
 [!code-cs[csProgGuideLINQ#31](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#31)]  
  
 请注意，如果未指定名称，则匿名类型将使用源元素的名称作为其属性名称。  若要为匿名类型中的属性指定新名称，请按如下方式编写 `select` 语句：  
  
```  
select new { First = student.FirstName, Last = student.LastName };  
```  
  
 如果您在上一个示例中这样做，则 `Console.WriteLine` 语句也必须更改：  
  
```  
Console.WriteLine(student.First + " " + student.Last);  
```  
  
## 编译代码  
  
-   若要运行这段代码，请将该类复制并粘贴到已经在 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 中创建的 Visual C\# 控制台应用程序项目中。  默认情况下，此项目针对 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 3.5 版，并且将具有一个对 System.Core.dll 的引用和一条针对 System.Linq 的 `using` 指令。  如果项目不满足上面的一个或多个要求，则您可以手动添加它们。  有关更多信息，请参见 [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)