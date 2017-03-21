---
title: "递归过程 (Visual Basic) | Microsoft Docs"
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
  - "函数 [Visual Basic], 递归调用"
  - "过程, 调用"
  - "过程, 递归的"
  - "过程, 自身调用"
  - "递归"
  - "递归过程"
  - "Visual Basic 代码, 过程"
ms.assetid: ba1d3962-b4c3-48d3-875e-96fdb4198327
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 递归过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

“递归”过程是指调用自身的过程。  通常，这不是编写 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 代码的最有效方法。  
  
 下面的过程使用递归计算其原始参数的阶乘：  
  
 [!code-vb[VbVbcnProcedures#51](./codesnippet/VisualBasic/recursive-procedures_1.vb)]  
  
## 使用递归过程时的注意事项  
 **限制条件**。  您在设计一个递归过程时，必须至少测试一个可以终止此递归的条件，并且还必须对在合理的递归调用次数内未满足此类条件的情况进行处理。  如果没有一个在正常情况下可以满足的条件，则过程将陷入执行无限循环的高度危险之中。  
  
 **内存使用**。  应用程序的局部变量所使用的空间有限。  过程在每次调用它自身时，都会占用更多的内存空间以保存其局部变量的附加副本。  如果这个进程无限持续下去，最终会导致 <xref:System.StackOverflowException> 错误。  
  
 **效率**。  几乎在任何情况下都可以用循环替代递归。  循环不会产生传递变量、初始化附加存储空间和返回值所需的开销，  因此使用循环相对于使用递归调用可以大幅提高性能。  
  
 **相互递归**。  如果两个过程相互调用，可能会使性能变差，甚至产生无限循环。  此类设计所产生的问题与单个递归过程所产生的问题相同，但更难检测和调试。  
  
 **调用时使用括号**。  当 `Function` 过程以递归方式调用它自身时，您必须在过程名称后加上括号（即使不存在参数列表）。  否则，函数名就会被视为表示函数的返回值。  
  
 **测试**。  在编写递归过程时，应非常细心地进行测试，以确保它总是能满足某些限制条件。  您还应该确保不会因为过多的递归调用而耗尽内存。  
  
## 请参阅  
 <xref:System.StackOverflowException>   
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [过程疑难解答](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [关于异常的疑难解答：System.StackOverflowException](../Topic/Troubleshooting%20Exceptions:%20System.StackOverflowException.md)