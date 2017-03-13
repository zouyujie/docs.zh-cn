---
title: "如何：在 Visual Basic 中将过程传递给另一过程 | Microsoft Docs"
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
  - "AddressOf 运算符"
  - "委托 [Visual Basic], 传递过程"
ms.assetid: 5adbba15-5a1d-413f-ab3e-3ff6cc0a4669
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 如何：在 Visual Basic 中将过程传递给另一过程
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例演示如何使用委托将过程传递给另一个过程。  
  
 委托是一种类型，与任何其他类型一样可在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中使用。  `AddressOf` 运算符如果应用到一个过程名，则返回一个委托对象。  
  
 此示例有一个具有委托参数的过程，该委托参数可接受对另一个过程的引用，而引用则是通过 `AddressOf` 运算符获得的。  
  
### 创建委托和匹配过程  
  
1.  创建一个名为 `MathOperator` 的委托。  
  
     [!code-vb[VbVbalrDelegates#1](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_1.vb)]  
  
2.  创建一个名为 `AddNumbers` 的过程，其参数和返回值与 `MathOperator` 的参数和返回值匹配，以使签名匹配。  
  
     [!code-vb[VbVbalrDelegates#2](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_2.vb)]  
  
3.  创建名为 `SubtractNumbers` 的过程，其签名与 `MathOperator` 匹配。  
  
     [!code-vb[VbVbalrDelegates#3](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_3.vb)]  
  
4.  创建一个名为 `DelegateTest` 的过程，它接受一个委托作为参数。  
  
     此过程可接受对 `AddNumbers` 或 `SubtractNumbers` 的引用，这是因为它们的签名与 `MathOperator` 签名匹配。  
  
     [!code-vb[VbVbalrDelegates#4](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_4.vb)]  
  
5.  创建一个名为 `Test` 的过程，它使用 `AddNumbers` 的委托作为参数调用 `DelegateTest` 一次，然后使用 `SubtractNumbers` 的委托作为参数再次调用。  
  
     [!code-vb[VbVbalrDelegates#5](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_5.vb)]  
  
     调用 `Test` 时，它首先显示 `AddNumbers` 对 `5` 和 `3` 的操作结果，也就是 8。  然后显示 `SubtractNumbers` 对 `9` 和 `3` 的操作结果，也就是 6。  
  
## 请参阅  
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [AddressOf 运算符](../../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Delegate 语句](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [如何：调用委托方法](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)