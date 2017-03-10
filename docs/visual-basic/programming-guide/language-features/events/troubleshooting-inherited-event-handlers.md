---
title: "有关 Visual Basic 中继承的事件处理程序的疑难解答 | Microsoft Docs"
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
  - "事件处理程序, 疑难解答"
  - "事件处理, 疑难解答"
  - "继承的事件"
  - "事件疑难解答"
  - "Visual Basic 疑难解答, 事件处理程序"
ms.assetid: e1c8759f-5370-4308-8476-8c48b73509bf
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 有关 Visual Basic 中继承的事件处理程序的疑难解答
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本主题列出了所继承组件中事件处理程序出现的常见问题。  
  
## 过程  
  
#### 对于每次调用，事件处理程序中的代码执行两次  
  
-   继承的事件处理程序不得包含 [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md) 子句。  基类中的方法已经与事件关联并将相应地激发事件。  从继承的方法中移除 `Handles` 子句。  
  
     [!code-vb[VbVbalrEvents#32](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#32)]  
  
-   如果继承的方法没有 `Handles` 关键字，请确保您的代码不包含额外的 [AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md) 或处理同一事件的任何其他方法。  
  
## 请参阅  
 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)