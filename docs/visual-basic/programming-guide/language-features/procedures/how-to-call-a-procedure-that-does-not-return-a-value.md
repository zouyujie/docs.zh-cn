---
title: "如何：调用不返回值的过程 (Visual Basic) | Microsoft Docs"
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
  - "过程调用, 返回值"
  - "过程, 调用"
  - "Visual Basic 代码, 过程"
ms.assetid: 259b49a3-a3c1-4254-ba8c-73cdc4127703
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 如何：调用不返回值的过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`Sub` 过程不向调用代码返回值。  使用独立调用语句显式调用该过程。  不能在表达式中仅使用其名称来调用它。  
  
### 调用 Sub 过程  
  
1.  指定 `Sub` 程序的名称。  
  
2.  请在过程名称后面用括号将参数列表括起来。  如果无任何参数，也可以选择省略括号。  但是，使用括号可使代码更容易阅读。  
  
3.  将参数放入括号内的参数列表中，以逗号分隔。  请确保按 `Sub` 过程定义对应的参数时的顺序提供变量。  
  
     下面的示例调用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> 函数激活应用程序窗口。  <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> 将窗口标题作为它的唯一参数。  它并不向调用代码返回值。  如果当前没有运行记事本进程，本示例将引发 <xref:System.ArgumentException>。  `Shell` 过程假定应用程序位于指定的路径中。  
  
     [!code-vb[VbVbalrCatRef#11](./codesnippet/VisualBasic/how-to-call-a-procedure-that-does-not-return-a-value_1.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Interaction.Shell%2A>   
 <xref:System.ArgumentException>   
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [如何：创建过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure.md)   
 [如何：调用返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-returns-a-value.md)   
 [如何：在 Visual Basic 中调用事件处理程序](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-event-handler.md)