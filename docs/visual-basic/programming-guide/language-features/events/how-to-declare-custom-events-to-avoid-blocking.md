---
title: "如何：声明自定义事件以避免阻止 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "自定义事件"
  - "声明事件, 自定义"
  - "事件 [Visual Basic], 自定义"
ms.assetid: 998b6a90-67c5-4d2c-8b11-366d3e355505
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 如何：声明自定义事件以避免阻止 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在几种情况下，一个事件处理程序不阻止后续的事件处理程序很重要。  自定义事件允许事件异步调用它的事件处理程序。  
  
 默认情况下，事件声明的后备存储字段是一个依次组合所有事件处理程序的多路广播委托。  这意味着，如果一个处理程序的完成时间很长，它将阻止其他处理程序，直到它完成为止。  （功能良好的事件处理程序应从不会执行冗长的或可能起阻止作用的操作。）  
  
 您可以不使用 Visual Basic 提供的默认事件实现功能，而是使用自定义事件异步执行事件处理程序。  
  
## 示例  
 在本示例中，`AddHandler` 访问器将 `Click` 事件的每个处理程序的委托添加到存储在 `EventHandlerList` 字段中的 <xref:System.Collections.ArrayList>。  
  
 在代码引发 `Click` 事件时，`RaiseEvent` 访问器将使用 <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A> 方法异步调用所有事件处理程序的委托。  该方法在辅助线程上调用每个处理程序并立即返回，这样处理程序便无法互相阻止。  
  
 [!code-vb[VbVbalrEvents#27](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-custom-events-to-avoid-blocking_1.vb)]  
  
## 请参阅  
 <xref:System.Collections.ArrayList>   
 <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>   
 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)   
 [如何：声明自定义事件以节省内存](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)