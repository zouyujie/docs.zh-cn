---
title: "RemoveHandler 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.RemoveHandlerMethod"
  - "vb.RemoveHandler"
  - "RemoveHandler"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "RemoveHandler 关键字"
  - "RemoveHandler 语句"
ms.assetid: 647cd825-e877-4910-b4f1-8d168beebe6a
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# RemoveHandler 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

移除事件与事件处理程序之间的关联。  
  
## 语法  
  
```  
RemoveHandler event, AddressOf eventhandler  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`event`|所处理的事件的名称。|  
|`eventhandler`|当前处理事件的过程的名称。|  
  
## 备注  
 `AddHandler` 和 `RemoveHandler` 语句使您可以在程序执行过程中的任何时候启动和停止特定事件的事件处理。  
  
> [!NOTE]
>  对于自定义事件，`RemoveHandler` 语句将调用事件的 `RemoveHandler` 访问器。  有关自定义事件的更多信息，请参见 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)。  
  
## 示例  
 [!code-vb[VbVbalrEvents#17](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#17)]  
  
## 请参阅  
 [AddHandler 语句](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/events.md)