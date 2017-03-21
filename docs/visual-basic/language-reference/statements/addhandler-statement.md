---
title: "AddHandler 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AddHandlerMethod"
  - "addhandler"
  - "vb.addhandler"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "AddHandler 语句"
ms.assetid: cfe69799-2a0f-42c0-a99e-09fed954da01
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# AddHandler 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在运行时将事件与事件处理程序相关联。  
  
## 语法  
  
```  
AddHandler event, AddressOf eventhandler  
```  
  
## 部件  
 `event`  
 要处理的事件的名称。  
  
 `eventhandler`  
 将处理事件的过程的名称。  
  
## 备注  
 `AddHandler` 和 `RemoveHandler` 语句使您可以在程序执行过程中的任何时候启动和停止事件处理。  
  
 `eventhandler` 过程的签名必须与事件 `event` 的签名相匹配。  
  
 `Handles` 关键字和 `AddHandler` 语句都允许您指定特定过程处理特定事件，但有一些不同。  `AddHandler` 语句在运行时将过程连接到事件。  在定义过程以指定它处理特定事件时，请使用 `Handles` 关键字。  有关更多信息，请参见 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)。  
  
> [!NOTE]
>  对于自定义事件，`AddHandler` 语句将调用事件的 `AddHandler` 访问器。  有关自定义事件的更多信息，请参见 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)。  
  
## 示例  
 [!code-vb[VbVbalrEvents#17](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/addhandler-statement_1.vb)]  
  
## 请参阅  
 [RemoveHandler 语句](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/events.md)