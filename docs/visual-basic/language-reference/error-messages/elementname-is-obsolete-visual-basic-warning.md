---
title: "“&lt;元素名&gt;”已过时（Visual Basic 警告） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40008"
  - "bc40008"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40008"
ms.assetid: 729e3eb5-76ac-4c55-9fdd-78350e0de55e
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# “&lt;元素名&gt;”已过时（Visual Basic 警告）
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

语句尝试访问已标记有 <xref:System.ObsoleteAttribute> 特性（指令会将其视为警告）的编程元素。  
  
 可以将任何编程元素标记为不再使用，方法是对该元素应用 <xref:System.ObsoleteAttribute>。  如果使用，可以将该特性的 <xref:System.ObsoleteAttribute.IsError%2A> 属性设置为 `True` 或 `False`。  如果将其设置为 `True`，则编译器将使用该元素的尝试视为错误。  如果将它设置为 `False` 或默认为 `False`，则在尝试使用该元素时编译器会发出警告。  
  
 默认情况下，该消息是条警告，原因是 <xref:System.ObsoleteAttribute> 的 <xref:System.ObsoleteAttribute.IsError%2A> 属性为 `False`。  有关隐藏警告或将警告视为错误的更多信息，请参见[在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC40008  
  
### 更正此错误  
  
-   确保源代码引用拼写的元素名称正确无误。  
  
## 请参阅  
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)