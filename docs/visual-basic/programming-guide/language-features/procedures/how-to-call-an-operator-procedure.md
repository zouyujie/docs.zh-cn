---
title: "如何：调用运算符过程 (Visual Basic) | Microsoft Docs"
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
  - "运算符重载"
  - "运算符过程, 调用"
  - "运算符 [Visual Basic], 重载"
  - "重载运算符, 调用"
  - "过程调用, 运算符重载"
  - "过程, 运算符"
  - "返回值, 运算符过程"
  - "语法, 运算符过程"
ms.assetid: 0dce42cc-f0b0-4c14-9f62-018b21f33497
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：调用运算符过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用表达式中的运算符符号调用一个运算符过程。  如果是转换运算符，可以调用 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)，将值从一种数据类型转换为另一种数据类型。  
  
 请勿显示调用运算符过程。  您只是在赋值语句或表达式中使用运算符或 `CType` 函数，方法与正常使用运算符相同。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 完成对运算符过程的调用。  
  
 在类或结构上定义一个运算符也称为重载运算符。  
  
### 调用运算符过程  
  
1.  以正常方式使用表达式中的运算符符号。  
  
2.  请确保操作数的数据类型适合于运算符，且顺序正确。  
  
3.  运算符按预期方式提供表达式的值。  
  
### 调用转换运算符过程  
  
1.  使用表达式内的 `CType`。  
  
2.  请确保操作数的数据类型适合于转换，且顺序正确。  
  
3.  `CType` 调用转换运算符过程，并返回转换后的值。  
  
## 示例  
 下面的示例创建两个 <xref:System.TimeSpan> 结构，并将它们加起来，然后将结果存储在第三个 <xref:System.TimeSpan> 结构中。  <xref:System.TimeSpan> 结构定义运算符过程，以重载多个标准运算符。  
  
 [!code-vb[VbVbcnProcedures#29](./codesnippet/VisualBasic/how-to-call-an-operator-procedure_1.vb)]  
  
 由于 <xref:System.TimeSpan> 重载标准 `+` 运算符，当它计算 `combinedSpan` 的值时，上面的示例将调用一个运算符过程。  
  
 有关调用转换运算符过程的示例，请参见 [如何：使用定义运算符的类](../../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)。  
  
## 编译代码  
 请确保所使用的类或结构定义了要使用的运算符。  
  
## 请参阅  
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：定义运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何：定义转换运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Widening](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [如何：声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)