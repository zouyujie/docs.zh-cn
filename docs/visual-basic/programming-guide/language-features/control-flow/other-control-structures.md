---
title: "其他控件结构 (Visual Basic) | Microsoft Docs"
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
  - "控件结构"
  - "语句 [Visual Basic], 控制流"
ms.assetid: 24b811f7-98ba-40ec-8dd3-4d528cfa4574
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 其他控件结构 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供的控制结构有助于释放资源或减少必须重复对象引用的次数。  
  
## Using...End Using 结构  
 `Using...End Using` 结构建立一个语句块，其中可以使用 SQL 连接之类的资源。  可以选择使用 `Using` 语句来获取资源。  退出 `Using` 块时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 自动释放资源以使这些资源可用于其他代码。  资源必须是本地的并且可释放。  有关更多信息，请参见 [Using 语句](../../../../visual-basic/language-reference/statements/using-statement.md)。  
  
## With...End With 结构  
 使用 `With...End With` 结构，您可以仅指定某个对象引用一次，然后运行一系列访问其成员的语句。  这可以简化代码并改善性能，这是因为 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 不必为访问引用的每条语句重新建立引用。  有关更多信息，请参见 [With...End With 语句](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)。  
  
## 请参阅  
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [决策结构](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [嵌套的控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Using 语句](../../../../visual-basic/language-reference/statements/using-statement.md)   
 [With...End With 语句](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)