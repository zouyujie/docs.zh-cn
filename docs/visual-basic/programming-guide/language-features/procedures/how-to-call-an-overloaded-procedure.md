---
title: "如何：调用重载过程 (Visual Basic) | Microsoft Docs"
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
  - "过程调用, 重载的"
  - "过程, 调用"
  - "过程, 多个版本"
  - "过程, 重载"
  - "Visual Basic 代码, 过程"
ms.assetid: 3bb331fb-f6bc-406f-9ca0-9609b497014c
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 如何：调用重载过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

重载过程的优点在于使调用更灵活。  调用代码可以获取它需要传递给过程的信息，然后调用单个过程名，无论它传递的是什么参数。  
  
### 调用定义了多个版本的过程  
  
1.  在调用代码中，确定哪些数据将传递给过程。  
  
2.  以通常方式编写过程调用，用参数列表提供数据。  请确保该变量与为过程定义的一种版本的参数列表匹配。  
  
3.  您不需要确定要调用过程的哪个版本。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会将控制传递给与参数列表匹配的版本。  
  
     下面的示例调用在 [如何：定义一个过程的多个版本](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md) 中声明的 `post` 过程。  它获取客户标识，确定它是 `String` 还是 `Integer`，然后在每一种情况下都调用相同的过程。  
  
     [!code-vb[VbVbcnProcedures#56](./codesnippet/VisualBasic/how-to-call-an-overloaded-procedure_1.vb)]  
  
     [!code-vb[VbVbcnProcedures#57](./codesnippet/VisualBasic/how-to-call-an-overloaded-procedure_2.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [过程疑难解答](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [如何：定义一个过程的多个版本](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [如何：重载带有可选参数的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何：重载参数数量不确定的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)