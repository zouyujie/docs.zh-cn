---
title: "如何：防止过程参数的值被更改 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], ByRef"
  - "变量 [Visual Basic], ByVal"
  - "变量 [Visual Basic], 更改值"
  - "变量 [Visual Basic], 按引用传递"
  - "变量 [Visual Basic], 按值传递"
  - "过程参数"
  - "过程参数"
  - "过程, 参数"
  - "过程, 调用"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: d2b7c766-ce16-4d2c-8d79-3fc0e7ba2227
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：防止过程参数的值被更改 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果过程声明参数， [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 为直接对基础调用代码中的编程元素的一个参数的程序代码。  这使得过程能够更改调用代码中作为实参基础的值。  有时调用代码可能需要防止此类更改。  
  
 可以通过声明对应的参数 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 始终防止实参更改在过程中。  如果您希望能够更改特定参数在某些情况下，但没有其他中，可以声明它 `ByRef` ，让调用代码确定在每个的传递机制调用。  它通过将对应的实参将执行该值，或者括号内不括在括号中而通过引用。  有关更多信息，请参见 [如何：强制通过值传递参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)。  
  
## 示例  
 下面的示例演示获取数组变量并对其元素的两个过程。  `increase` 程序每个元素加。  `replace` 过程将新数组赋给参数 `a()` 然后每个元素加。  但是，重新分配并不会影响调用代码中的基础数组变量。  
  
 [!code-vb[VbVbcnProcedures#35](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-protect-a-procedu_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#38](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-protect-a-procedu_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#37](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-protect-a-procedu_3.vb)]  
  
 第一 `MsgBox` 调用显示 “after increase\(n\):11， 21， 31， 41 "。  由于数组`n`是引用类型，`replace`可以更改其成员，因此，即使传递机制为 `ByVal`。  
  
 第二 `MsgBox` 调用显示 “after replace\(n\):11， 21， 31， 41 "。  由于`n`通过 `ByVal`，`replace`无法通过将新数组更改调用代码中的变量的`n`到它。  当`replace`创建新的数组实例`k`并将其赋给局部变量`a`时，它将丢失对`n`已通过调用代码。  当更改`a`的成员，因此，只有局部数组`k`受到影响。  因此，`replace`不会使数组`n`的值在调用代码中。  
  
## 编译代码  
 在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 的默认值是通过值传递实参。  但是，好的编程习惯。声明每个 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 形参或 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 关键字。  这将使您的代码更容易阅读。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [如何：将参数传递给过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [通过值传递参数和通过引用传递参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [如何：更改过程参数的值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [如何：强制通过值传递参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)