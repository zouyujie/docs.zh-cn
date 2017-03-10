---
title: "WithEvents (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.WithEvents"
  - "WithEvents"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "WithEvents 关键字"
ms.assetid: 19d461f5-d72f-4de9-8c1d-0a6650316990
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# WithEvents (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定一个或多个已声明成员变量引用可引发事件的类的实例。  
  
## 备注  
 当某个变量是使用 `WithEvents` 定义时，您可以用声明方式指定某个方法使用 `Handles` 关键字处理该变量的事件。  
  
 您只能在类或模块级别使用 `WithEvents`。  这意味着 `WithEvents` 变量的声明上下文必须是类或模块，不能是源文件、命名空间、结构或过程。  
  
 您不能对结构成员使用 `WithEvents`。  
  
 您只能使用 `WithEvents` 声明单个变量，不能声明数组。  
  
## 规则  
  
-   **元素类型。**您必须将 `WithEvents` 变量声明成为对象变量，以便它们可以接受类实例。  但是，您不能将它们声明为 `Object`。  必须将它们声明为可以引发事件的特定类。  
  
 `WithEvents` 修饰符可用于下面的上下文中：[Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
## 请参阅  
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/events.md)