---
title: "串联运算符 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "& 运算符 [Visual Basic], 串联"
  - "+ 运算符 [Visual Basic], 串联"
  - "串联运算符"
  - "串联运算符, Visual Basic 字符串"
  - "运算符 [Visual Basic], 串联"
  - "Visual Basic 代码, 运算符"
ms.assetid: e59908c3-89e0-41ae-933d-3e8826c16a04
caps.latest.revision: 18
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 串联运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

串联运算符将多个字符串联接为一个字符串。  有两种串联运算符：`+` 和 `&`。  这两种串联运算符都执行基本的串联运算，如下面的示例所示。  
  
 [!CODE [Dim x As String = "Mic" & "ro" & "soft" Dim y As String = "Mic" + "ro" + "soft" ' The preceding statements set both x and y to "Microsoft".](Dim x As String = "Mic" & "ro" & "soft" Dim y As String = "Mic" + "ro" + "soft" ' The preceding statements set both x and y to "Microsoft".)]  
  
 这两种运算符还可以串联 `String` 变量，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators#76](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/concatenation-operators_1.vb)]  
  
## 两种串联运算符之间的区别  
 [\+ 运算符](../../../../visual-basic/language-reference/operators/addition-operator.md) 的主要用途是将两个数字相加。  然而，它还可以将数值操作数与字符串操作数串联起来。  `+` 操作数具有一套复杂的规则，用来确定是相加、串联、指示编译器错误还是引发运行时的 <xref:System.InvalidCastException> 异常。  
  
 [& 运算符](../../../../visual-basic/language-reference/operators/concatenation-operator.md) 仅定义用于 `String` 操作数，而且无论 `Option Strict` 的设置是什么，都会将其操作数扩展到 `String`。  对于字符串串联操作，建议使用 `&` 运算符，原因是它以独占方式为字符串定义，并降低产生意外转换的可能性。  
  
## 性能：字符串和 StringBuilder  
 如果你对字符串执行大量操作（如串联、删除或替换），则通过 <xref:System.Text> 命名空间中的 <xref:System.Text.StringBuilder> 类可能会提高性能。  该类采用额外指令来创建和初始化 <xref:System.Text.StringBuilder> 对象，并且使用其他指令将其最终值转换为 `String`，但此时你可能会恢复使用 <xref:System.Text.StringBuilder>，因为它的执行速度更快。  
  
## 请参阅  
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [字符串操作方法的类型 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/types-of-string-manipulation-methods.md)   
 [算术运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)