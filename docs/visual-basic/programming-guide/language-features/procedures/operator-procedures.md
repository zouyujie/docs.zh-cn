---
title: "运算符过程 (Visual Basic) | Microsoft Docs"
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
  - "运算符过程"
  - "运算符 [Visual Basic], 重载"
  - "重载运算符"
  - "过程, 运算符"
  - "语法, 运算符过程"
  - "Visual Basic 代码, 运算符"
  - "Visual Basic 代码, 过程"
ms.assetid: 8c513d38-246b-4fb7-8b75-29e1364e555b
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 运算符过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

运算符过程是一系列 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 语句，这些语句在您所定义的类或结构上定义标准运算符（例如 `*`、`<>` 或 `And`）的行为。  这也称为“运算符重载”。  
  
## 何时定义运算符过程  
 当您定义好类或结构后，可以将变量声明为所定义的类或结构的类型。  有时，这样的变量需要作为表达式的一部分参与到运算中。  若要执行此操作，它必须是运算符的一个操作数。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 仅在其基本数据类型上定义运算符。  在一个或两个操作数都是您的类或结构的类型时，可以定义一个运算符的行为。  
  
 有关更多信息，请参见 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)。  
  
## 运算符过程的类型  
 运算符过程可以是下面的一种类型：  
  
-   一元运算符的定义，其中的参数是您的类或结构的类型。  
  
-   一个二元运算符的定义，其中至少一个参数是您的类或结构的类型。  
  
-   一个转换运算符的定义，其中的参数是您的类或结构的类型。  
  
-   一个转换运算符的定义，返回您的类或结构的类型。  
  
 转换运算符总是一元运算符，您也总是将 `CType` 用作所定义的运算符。  
  
## 声明语法  
 声明运算符过程的语法如下所示：  
  
 `Public Shared`   `[Widening | Narrowing]`   `Operator`   ``  *operatorsymbol*  `(` *operand1*  `[,`  *operand2* `]) As`  *datatype*  
  
 `' Statements of the operator procedure.`  
  
 `End Operator`  
  
 仅在类型转换运算符上使用 `Widening` 或 `Narrowing` 关键字。  类型转换运算符的符号总是 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)。  
  
 声明两个操作数以定义一个二元运算符，声明一个操作数以定义一个一元运算符（包括类型转换运算符）。  所有操作数都必须声明为 `ByVal`。  
  
 用与声明 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 的参数相同的方法声明每个操作数。  
  
### 数据类型  
 因为是在已定义的类或结构上定义运算符，所以至少其中一个操作数必须是该类或结构的数据类型。  对于类型转换运算符，操作数或返回类型必须是类或结构的数据类型。  
  
 有关更多详细信息，请参见[Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)。  
  
## 调用语法  
 使用表达式中的运算符符号隐式调用运算符过程。  按照为预定义运算符提供操作数的方法提供操作数。  
  
 隐式调用运算符过程的语法如下所示：  
  
 `Dim testStruct As`  *结构名*  
  
 `Dim testNewStruct As`  *structurename*  `= testStruct`  *operatorsymbol*  `10`  
  
### 声明与调用阐释  
 下面的结构将有符号的 128 位整数值存储为高序部分和低序部分。  它将 `+` 运算符定义为将两个 `veryLong` 值相加并生成结果 `veryLong` 值。  
  
 [!code-vb[VbVbcnProcedures#23](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/operator-procedures_1.vb)]  
  
 下面的示例演示对 `veryLong` 上定义的 `+` 运算符的典型调用。  
  
 [!code-vb[VbVbcnProcedures#24](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/operator-procedures_2.vb)]  
  
 有关更多信息和示例，请参见 [Operator Overloading in Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703)（Visual Basic 2005 中的运算符重载）。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Operator 语句](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [如何：定义运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何：定义转换运算符](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [如何：调用运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [如何：使用定义运算符的类](../../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)