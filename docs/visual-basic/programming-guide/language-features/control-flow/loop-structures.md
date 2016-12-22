---
title: "循环结构 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "条件语句, 循环结构"
  - "控制流, 循环"
  - "Do 语句, Do 循环"
  - "For 关键字 [Visual Basic], 循环结构"
  - "循环结构"
  - "循环"
  - "语句 [Visual Basic], 循环"
ms.assetid: ecacb09b-a4c9-42be-98b2-a15d368b5db8
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 循环结构 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 循环结构允许您重复运行一行或多行代码。  您可以用循环结构重复执行语句，直到条件为 `True`、直到条件为 `False`、执行了指定的次数，或者为集合中的每个元素各执行一次语句。  
  
 下图显示一个循环结构，该结构运行一组语句直到条件变为 true。  
  
 ![Do...Until 循环流程图](../../../../visual-basic/programming-guide/language-features/control-flow/media/dountilloop.gif "DoUntilLoop")  
运行一组语句直到条件变为 true  
  
## while 循环  
 只要 `While` 语句中指定的条件为 `True`，`While`...`End While` 构造就会运行一组语句。  有关更多信息，请参见 [While...End While 语句](../../../../visual-basic/language-reference/statements/while-end-while-statement.md)。  
  
## Do 循环  
 `Do`...`Loop` 构造允许您在循环结构的开始或结尾对条件进行测试。  您还可以指定在条件保持为 `True` 或直到条件变为 `True` 时是否重复循环。  有关更多信息，请参见 [Do...Loop 语句](../../../../visual-basic/language-reference/statements/do-loop-statement.md)。  
  
## for 循环  
 `For`...`Next` 构造按设置好的次数执行循环。  它使用循环控制变量（也称为*“计数器”*）跟踪重复。  您可以指定此计数器的起始值和终止值，并可以选择指定计数器从一个重复到下一个重复递增的数量。  有关更多信息，请参见 [For...Next 语句](../../../../visual-basic/language-reference/statements/for-next-statement.md)。  
  
## For Each 循环  
 `For Each`...`Next` 构造为集合中的每个元素运行一次一组语句。  您指定循环控制变量，但不必确定它的起始值或终止值。  有关更多信息，请参见 [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)。  
  
## 请参阅  
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [决策结构](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [其他控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)   
 [嵌套的控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)