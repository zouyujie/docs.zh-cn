---
title: "事件“&lt;事件名 1&gt;”无法实现接口“&lt;接口&gt;”上的事件“&lt;事件名 2&gt;”，因为它们的委托类型“&lt;委托 1&gt;”和“&lt;委托 2&gt;”不匹配 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31423"
  - "bc31423"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31423"
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 事件“&lt;事件名 1&gt;”无法实现接口“&lt;接口&gt;”上的事件“&lt;事件名 2&gt;”，因为它们的委托类型“&lt;委托 1&gt;”和“&lt;委托 2&gt;”不匹配
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 无法实现某个事件，因为该事件的委托类型与接口中事件的委托类型不匹配。  如果在接口中定义了多个事件，然后尝试用一个事件同时实现这些事件，则可能发生此错误。  只有当所有要实现的事件都使用 `As` 语法进行声明并指定相同的委托类型时，事件才能实现两个或多个事件。  
  
 **错误 ID：**BC31423  
  
### 更正此错误  
  
-   单独实现事件。  
  
     \- 或 \-  
  
-   使用 `As` 语法定义接口中的事件并指定相同的委托类型。  
  
## 请参阅  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/events.md)