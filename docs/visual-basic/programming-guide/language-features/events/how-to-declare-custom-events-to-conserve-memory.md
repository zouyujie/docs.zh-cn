---
title: "如何：声明自定义事件以节省内存 (Visual Basic) | Microsoft Docs"
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
ms.assetid: 87ebee87-260c-462f-979c-407874debd19
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：声明自定义事件以节省内存 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在几种情况下，应用程序保持低的内存使用率很重要。  自定义事件允许应用程序只为它处理的事件而使用内存。  
  
 默认情况下，当类声明事件时，编译器会将内存分配给一个字段，以存储事件信息。  如果类具有许多未使用的事件，则它们会不必要地占用内存。  
  
 您可以不使用 Visual Basic 提供的默认事件实现功能，而是使用自定义事件更细致地管理内存使用情况。  
  
## 示例  
 在本示例中，类使用 <xref:System.ComponentModel.EventHandlerList> 类的一个实例（存储在 `Events` 字段中），以存储有关使用中的事件的信息。  <xref:System.ComponentModel.EventHandlerList> 类是一个经过优化的列表类，专为保存委托而设计。  
  
 此类中的所有事件均使用 `Events` 字段来跟踪哪些方法正处理哪个事件。  
  
 [!code-vb[VbVbalrEvents#22](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#22)]  
  
## 请参阅  
 <xref:System.ComponentModel.EventHandlerList>   
 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)   
 [如何：声明自定义事件以避免阻止](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)