---
title: "表达式的类型为“&lt;类型名&gt;”，这是受限类型，不能用于访问从“Object”或“ValueType”继承的成员 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc31393"
  - "vbc31393"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31393"
ms.assetid: 2963cf3f-c527-4aa7-b67c-ee80b6d23186
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 表达式的类型为“&lt;类型名&gt;”，这是受限类型，不能用于访问从“Object”或“ValueType”继承的成员
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

表达式计算得出的类型无法被公共语言运行时 \(CLR\) 装箱，但可以访问要求装箱的成员。  
  
 *“装箱”*指需要将一个类型转换为 `Object`，或偶尔转换为 <xref:System.ValueType> 的处理过程。  公共语言运行时无法对某些结构类型装箱，例如 <xref:System.ArgIterator>、<xref:System.RuntimeArgumentHandle> 和 <xref:System.TypedReference>。  
  
 此表达式尝试使用受限制的类型，以调用从 <xref:System.Object> 或 <xref:System.ValueType> 继承的方法，如 <xref:System.Object.GetHashCode%2A> 或 <xref:System.Object.ToString%2A>。  为访问此方法，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 已尝试隐式装箱导致此错误的转换。  
  
 **错误 ID：**BC31393  
  
### 更正此错误  
  
1.  找到计算结果为引证类型的表达式。  
  
2.  查找语句中尝试调用从 <xref:System.Object> 或 <xref:System.ValueType> 继承的方法的部分。  
  
3.  重写语句，以避免进行方法调用。  
  
## 请参阅  
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)