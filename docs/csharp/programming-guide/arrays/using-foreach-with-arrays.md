---
title: "对数组使用 foreach（C# 编程指南） | Microsoft Docs"
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
  - "数组 [C#], foreach"
  - "foreach 语句 [C#], 与数组一起使用"
ms.assetid: 5f2da2a9-1f56-4de5-94cc-e07f4f7a0244
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 对数组使用 foreach（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

C\# 还提供 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 语句。  该语句提供一种简单、明了的方法来循环访问数组或任何可枚举集合的元素。  `foreach` 语句按数组或集合类型的枚举器返回的顺序处理元素，该顺序通常是从第 0 个元素到最后一个元素。  例如，以下代码创建一个名为 `numbers` 的数组，并使用 `foreach` 语句循环访问该数组：  
  
 [!code-cs[csProgGuideArrays#28](../../../csharp/programming-guide/arrays/codesnippet/CSharp/using-foreach-with-arrays_1.cs)]  
  
 借助多维数组，你可以使用相同的方法来循环访问元素，例如：  
  
 [!code-cs[csProgGuideArrays#29](../../../csharp/programming-guide/arrays/codesnippet/CSharp/using-foreach-with-arrays_2.cs)]  
  
 但对于多维数组，使用嵌套的 [for](../../../csharp/language-reference/keywords/for.md) 循环可以更好地控制数组元素。  
  
## 请参阅  
 <xref:System.Array>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [数组](../../../csharp/programming-guide/arrays/index.md)   
 [一维数组](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [多维数组](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)   
 [交错数组](../../../csharp/programming-guide/arrays/jagged-arrays.md)