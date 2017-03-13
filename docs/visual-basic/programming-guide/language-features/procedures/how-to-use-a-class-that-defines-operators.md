---
title: "如何：使用定义运算符的类 (Visual Basic) | Microsoft Docs"
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
  - "示例 [Visual Basic], CType"
  - "运算符重载"
  - "运算符过程, 调用"
  - "运算符 [Visual Basic], 重载"
  - "过程, 调用"
  - "过程, 运算符"
  - "返回值, 运算符过程"
  - "语法, 运算符过程"
ms.assetid: 7ccce94a-6ca0-47d1-9f3f-13385d34f5d5
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 如何：使用定义运算符的类 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果使用定义了自己的运算符的类或结构，则可以从 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 访问这些运算符。  
  
 在类或结构上定义一个运算符也称为重载运算符。  
  
## 示例  
 下面的示例访问 SQL 结构 <xref:System.Data.SqlTypes.SqlString>，它定义了 SQL 字符串和 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 字符串之间的双向转换运算符 \([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)\)。  使用 `CType(`*SQL 字符串表达式*, `String)` 将 SQL 字符串转换为 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 字符串，而使用 `CType(`*Visual Basic 字符串表达式*, <xref:System.Data.SqlTypes.SqlString>`)` 执行反向转换。  
  
 [!code-vb[VbVbcnProcedures#30](./codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#31](./codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_2.vb)]  
  
 <xref:System.Data.SqlTypes.SqlString> 结构定义从 `String` 到 <xref:System.Data.SqlTypes.SqlString> 的转换运算符 \([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)\)，以及从 <xref:System.Data.SqlTypes.SqlString> 到 `String` 的另一个转换运算符。  将 `title` 赋给 `jobTitle` 的语句使用第一个运算符，而 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 函数调用使用第二个运算符。  
  
## 编译代码  
 请确保所使用的类或结构定义了要使用的运算符。  不要假设类或结构已经定义每个可进行重载的运算符。  有关可用运算符的列表，请参见 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)。  
  
 请在源文件的开头添加相应于 SQL 字符串的 `Imports` 语句（在本例中为 <xref:System.Data.SqlTypes>）。  
  
 项目必须具有对 System.Data 和 System.XML 的引用。  
  
## 请参阅  
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：定义运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何：定义转换运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [如何：调用运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [Widening](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Structure 语句](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [如何：声明结构](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)