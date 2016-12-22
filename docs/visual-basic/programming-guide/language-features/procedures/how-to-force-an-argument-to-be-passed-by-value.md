---
title: "如何：强制通过值传递参数 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], ByVal"
  - "变量 [Visual Basic], 更改值"
  - "变量 [Visual Basic], 在括号中"
  - "变量 [Visual Basic], 按值传递"
  - "过程参数"
  - "过程参数, 在括号中"
  - "过程参数"
  - "过程, 参数"
  - "过程, 调用"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 77b4f2d2-1055-4c2f-a521-874d1db86946
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：强制通过值传递参数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

过程声明确定传递机制。  如果形参声明 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)为， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 所需引用传递对应的实参。  这使得过程能够更改调用代码中该编程元素的值参数。  如果希望保护基础元素避免这种更改，可以重写传入的 `ByRef` framework 通过用括号将参数名称过程调用。  这些括号是除了包括实参列表的括号之外调用。  
  
 调用代码无法重写机制。 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)  
  
### 强制通过值传递实参  
  
-   如果对应的形参声明一个程序的 `ByVal` ，则无需执行任何其他步骤。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 已经预期通过值传递实参  
  
-   如果对应的形参声明一个程序的 `ByRef` ，请将实参包括在括号内在过程调用。  
  
## 示例  
 下面的示例重写 `ByRef` 参数声明。  在强制 `ByVal`的调用，请注意括号的两个级别。  
  
 [!CODE [VbVbcnProcedures#39](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#39)]  
  
 [!CODE [VbVbcnProcedures#40](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#40)]  
  
 当 `str` 的对齐中的额外括号将参数列表， `setNewString` 程序不能在调用代码中更改它的值，并且， `MsgBox` 显示 “不能替换，如果传入的 ByVal”。  当 `str` 在额外括号中时没有包含，过程可以更改此值，并且， `MsgBox` 显示 “这是 inString 参数的一个新值”。  
  
## 编译代码  
 当通过引用传递变量时，必须使用 `ByRef` 关键字指定此机制。  
  
 在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 的默认值是通过值传递实参。  但是，好的编程习惯。声明每个 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 形参或 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 关键字。  这将使您的代码更容易阅读。  
  
## 可靠编程  
 如果过程声明参数 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)，代码的正确执行可能依赖于能够更改调用代码中的基础元素。  如果调用代码通过将实参括在括号内重写此调用机制，或者，如果它通过不可更改参数，则过程不能更改基础元素。  这可能会在调用代码中产生意外的结果。  
  
## .NET Framework 安全性  
 始终有允许程序的一个风险能够更改调用代码中作为实参基础的值。  请确保您希望此值更改为和准备签出对使用。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [如何：将参数传递给过程](../Topic/How%20to:%20Pass%20Arguments%20to%20a%20Procedure%20\(Visual%20Basic\).md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [通过值传递参数和通过引用传递参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [如何：更改过程参数的值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [如何：防止过程参数的值被更改](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)