---
title: "如何：创建嵌套组（C# 编程指南） | Microsoft Docs"
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
  - "对 LINQ 查询中的组进行分组"
  - "对 LINQ 查询分组"
  - "分组 [C# 中的 LINQ], 嵌套"
  - "嵌套查询 [C#]"
  - "查询 [C# 中的 LINQ], 嵌套组"
  - "查询表达式 [C# 中的 LINQ], 嵌套组"
ms.assetid: f48c64af-6d4e-473c-ab27-02f78b5ec2b9
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：创建嵌套组（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

下面的示例演示如何在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] 查询表达式中创建嵌套组。  对根据学生年级创建的每个组，将根据每个人的姓名进一步划分为小组。  
  
## 示例  
 [!code-cs[csProgGuideLINQ#24](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-create-a-nested-group_1.cs)]  
  
 请注意，需要使用三个嵌套的 `foreach` 循环来循环访问嵌套组的内部元素。  
  
## 编译代码  
 此示例包含对[如何：查询对象集合](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md)内示例应用程序中定义的对象的引用。  若要编译和运行此方法，请将它粘贴到该应用程序的 `StudentClass` 类中，并且在 `Main` 方法中添加对它的调用。  
  
 在改写此方法以适合您自己的应用程序时，请记住 LINQ 需要 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 3.5 版，并且项目必须包含一个对 System.Core.dll 的引用和一条针对 System.Linq 的 using 指令。  LINQ to SQL、LINQ to XML 和 LINQ to DataSet 类型需要其他 using 指令和引用。  有关更多信息，请参见 [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)