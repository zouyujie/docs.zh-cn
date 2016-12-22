---
title: "数组（C# 编程指南） | Microsoft Docs"
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
  - "数组 [C#]"
  - "C# 语言, 数组"
ms.assetid: bb79bdde-e570-4c30-adb0-1dd5759ae041
caps.latest.revision: 33
caps.handback.revision: 33
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 数组（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

可以在一个数组数据结构中存储同一类型的多个变量。  通过指定其元素的类型声明数组。  
  
 `type[] arrayName;`  
  
 下面的示例创建一维、多维和交错数组：  
  
 [!code-cs[csProgGuideArrays#1](../../../csharp/programming-guide/arrays/codesnippet/CSharp/index_1.cs)]  
  
## 数组概述  
 数组具有以下属性：  
  
-   数组可以是[一维](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)、[多维](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)或[交错](../../../csharp/programming-guide/arrays/jagged-arrays.md)的。  
  
-   当创建了数组实例时，将建立维度数和每个维度的长度。  在实例的生存期内，这些值不能更改。  
  
-   数值数组元素的默认值设置为零，而引用元素的默认值设置为 null。  
  
-   交错数组是数组的数组，因此其元素是引用类型并初始化为 `null`。  
  
-   数组的索引从零开始：具有 `n` 个元素的数组的索引是从 `0` 到 `n-1`。  
  
-   数组元素可以是任何类型，包括数组类型。  
  
-   数组类型是从抽象基类型 <xref:System.Array> 派生的[引用类型](../../../csharp/language-reference/keywords/reference-types.md)。  由于此类型实现了 <xref:System.Collections.IEnumerable> 和 <xref:System.Collections.Generic.IEnumerable%601>，因此可以对 C\# 中的所有数组使用 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 迭代。  
  
## 相关章节  
  
-   [作为对象的数组](../../../csharp/programming-guide/arrays/arrays-as-objects.md)  
  
-   [对数组使用 foreach](../../../csharp/programming-guide/arrays/using-foreach-with-arrays.md)  
  
-   [将数组作为参数传递](../../../csharp/programming-guide/arrays/passing-arrays-as-arguments.md)  
  
-   [使用 ref 和 out 传递数组](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)  
  
-   [More About Variables](http://go.microsoft.com/fwlink/?LinkId=221214)（有关变量的更多信息）位于[Beginning Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221230)（开始 Visual C\# 2010）中  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [Array Collection Type](http://msdn.microsoft.com/zh-cn/8a9964de-8941-47b1-a3cf-a01bc88db9e8)