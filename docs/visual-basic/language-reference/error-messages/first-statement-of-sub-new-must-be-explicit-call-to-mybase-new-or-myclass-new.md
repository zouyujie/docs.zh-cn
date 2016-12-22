---
title: "此“Sub New”的第一条语句必须是对“MyBase.New”或“MyClass.New”的显式调用，因为“&lt;派生的类名&gt;”的基类“&lt;基类名&gt;”中的“&lt;结构名&gt;”被标记为已过时：“&lt;错误消息&gt;” | Microsoft Docs"
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
  - "vbc30920"
  - "bc30920"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30920"
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 此“Sub New”的第一条语句必须是对“MyBase.New”或“MyClass.New”的显式调用，因为“&lt;派生的类名&gt;”的基类“&lt;基类名&gt;”中的“&lt;结构名&gt;”被标记为已过时：“&lt;错误消息&gt;”
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

类构造函数未明确调用基类构造函数，而隐式基类构造函数标记有 <xref:System.ObsoleteAttribute> 特性，指令会将其视为错误。  
  
 在派生类构造函数未调用基类构造函数时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 尝试生成对无参数基类构造函数的隐式调用。  如果在基类中没有无需参数即可调用的可访问构造函数，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 无法生成隐式调用。  在此情况下，将用 <xref:System.ObsoleteAttribute> 特性标记所需的构造函数，因此 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 无法调用它。  
  
 可以将任何编程元素标记为不再使用，方法是对该元素应用 <xref:System.ObsoleteAttribute>。  如果使用，可以将该特性的 <xref:System.ObsoleteAttribute.IsError%2A> 属性设置为 `True` 或 `False`。  如果将其设置为 `True`，则编译器将使用该元素的尝试视为错误。  如果将它设置为 `False` 或默认为 `False`，则在尝试使用该元素时编译器会发出警告。  
  
 **错误 ID：**BC30920  
  
### 更正此错误  
  
1.  检查带引号的错误信息并采取适当的操作。  
  
2.  将对 `MyBase.New()` 或 `MyClass.New()` 的调用作为 `Sub New` 的第一个语句包括在派生类中。  
  
## 请参阅  
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)