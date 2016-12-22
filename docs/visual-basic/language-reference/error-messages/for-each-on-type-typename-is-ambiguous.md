---
title: "类型“&lt;类型名&gt;”的“For Each”不明确，因为此类型实现了“System.Collections.Generic.IEnumerable(Of T)”的多个实例化 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc32096"
  - "bc32096"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32096"
ms.assetid: ed20d09c-913f-482e-89f8-c0a596c3ec24
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 类型“&lt;类型名&gt;”的“For Each”不明确，因为此类型实现了“System.Collections.Generic.IEnumerable(Of T)”的多个实例化
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`For Each` 语句指定包含多个 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法的迭代器变量。  
  
 迭代器变量所属的类型必须在 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 的其中一个 `Collections` 命名空间中实现 <xref:System.Collections.IEnumerable?displayProperty=fullName> 或 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> 接口。  通过对每个构造使用不同类型参数，类可以实现构造的多个泛型接口。  如果实现多个泛型接口的类用于迭代器变量，该变量将包含多个 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法。  在此情况下，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 无法选择要调用的方法。  
  
 **错误 ID：**BC32096  
  
### 更正此错误  
  
-   使用 [DirectCast 运算符](../../../visual-basic/language-reference/operators/directcast-operator.md) 或 [TryCast 运算符](../../../visual-basic/language-reference/operators/trycast-operator.md) 将迭代器变量类型强制转换成用于定义要使用的 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法的接口。  
  
## 请参阅  
 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)