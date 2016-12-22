---
title: "如何：更改过程参数的值 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], ByRef"
  - "变量 [Visual Basic], ByVal"
  - "变量 [Visual Basic], 更改值"
  - "变量 [Visual Basic], 按引用传递"
  - "变量 [Visual Basic], 按值传递"
  - "过程参数"
  - "过程参数"
  - "过程, 参数"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 6fad2368-5da7-4c07-8bf8-0f4e65a1be67
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：更改过程参数的值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

当调用过程时，您提供的每个参数对应于过程定义的一个参数。  在某些情况下，过程代码可能能够更改调用代码中作为实参基础的值。  在某些情况下，过程可以更改实参的本地副本。  
  
 当调用过程时， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 进行传递 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)的本地副本每个参数。  为传递的每 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)个参数， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 为直接对基础调用代码中的编程元素的一个参数的程序代码。  
  
 如果在调用代码中的基础元素是一个可修改元素，并传递 `ByRef`，过程代码可以使用直接引用更改调用代码中元素的值。  
  
## 更改基础值  
  
#### 更改过程实参的基础值在调用代码中  
  
1.  在过程声明中，为参数指定 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 与实参对应。  
  
2.  在调用代码中，将可修改的编程元素作为参数。  
  
3.  在调用代码中，不要将实参括号中的参数列表。  
  
4.  在过程代码中，使用形参名称将值赋给调用代码中的基础元素。  
  
 为演示进一步参见示例滚动。  
  
## 更改本地副本  
 如果在调用代码中的基础元素是不可更改元素，或者，如果传递 `ByVal`，则过程不能在调用代码中更改它的值。  但是，过程可以更改这样实参的本地副本。  
  
#### 更改过程实参的副本在程序代码中  
  
1.  在过程声明中，为参数指定 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 与实参对应。  
  
     \- 或 \-  
  
     在调用代码中，将实参括号中的参数列表。  这可以强制 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 传递参数值，因此，即使相应的参数指定 `ByRef`。  
  
2.  在过程代码中，使用形参名称将值赋给实参的本地副本。  不更改调用代码中的基础值。  
  
## 示例  
 下面的示例演示获取数组变量并对其元素的两个过程。  `increase` 程序每个元素加。  `replace` 过程将新数组赋给参数 `a()` 然后每个元素加。  
  
 [!CODE [VbVbcnProcedures#35](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#35)]  
  
 [!CODE [VbVbcnProcedures#36](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#36)]  
  
 [!CODE [VbVbcnProcedures#37](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#37)]  
  
 第一 `MsgBox` 调用显示 “after increase\(n\):11， 21， 31， 41 "。  由于数组`n`是引用类型，`replace`可以更改其成员，因此，即使传递机制为 `ByVal`。  
  
 第二 `MsgBox` 调用显示 “after replace\(n\):101， 201， 301 "。  由于 `n` 通过 `ByRef`，`replace`能更改调用代码中的变量的`n`并将一个新数组赋给它。  由于`n`是引用类型，`replace`还可以更改其成员。  
  
 可以防止过程更改调用代码中的变量。  请参见 [如何：防止过程参数的值被更改](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)。  
  
## 编译代码  
 当通过引用传递变量时，必须使用 `ByRef` 关键字指定此机制。  
  
 在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 的默认值是通过值传递实参。  但是，好的编程习惯。声明每个 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 形参或 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 关键字。  这将使您的代码更容易阅读。  
  
## .NET Framework 安全性  
 始终有允许程序的一个风险能够更改调用代码中作为实参基础的值。  请确保您希望此值更改为和准备签出对使用。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [如何：将参数传递给过程](../Topic/How%20to:%20Pass%20Arguments%20to%20a%20Procedure%20\(Visual%20Basic\).md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [可修改和不可修改参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [通过值传递参数和通过引用传递参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [如何：防止过程参数的值被更改](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [如何：强制通过值传递参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)