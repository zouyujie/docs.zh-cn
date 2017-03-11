---
title: "Visual Basic 中的运算符和表达式 | Microsoft Docs"
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
  - "表达式 [Visual Basic]"
  - "操作数"
  - "操作数, 定义"
  - "运算符 [Visual Basic]"
  - "运算符 [Visual Basic], 操作数"
  - "Visual Basic 代码, 表达式"
  - "Visual Basic 代码, 运算符"
ms.assetid: b86f3131-94ee-448f-96cd-79611e028b26
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Visual Basic 中的运算符和表达式
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

运算符是一种代码元素，可在一个或多个容纳值的代码元素上执行运算。  值元素包括变量、常量、文本、属性、`Function` 和 `Operator` 过程的返回值以及表达式。  
  
 表达式是与运算符组合在一起的一系列值元素，它将产生一个新值。  运算符通过执行计算、比较或其他运算来处理值元素。  
  
## 运算符的类型  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了以下类型的运算符：  
  
-   [算术运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)对数值执行常见计算，其中包括将数值的位模式移位。  
  
-   [比较运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)比较两个表达式，并返回表示比较结果的 `Boolean` 值。  
  
-   [串联运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)将多个字符串联接为一个字符串。  
  
-   [Visual Basic 中的逻辑和按位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)合并 `Boolean` 值或数值，并返回数据类型与这些值相同的结果。  
  
 与运算符组合在一起的值元素称为该运算符的操作数。  运算符与值元素组合在一起就形成了表达式，但赋值运算符除外，它将组成语句。  有关更多信息，请参见 [语句](../../../../visual-basic/programming-guide/language-features/statements.md)。  
  
## 表达式的求值  
 表达式的最终结果表示一个值，该值通常是某种常见的数据类型，如 `Boolean`、`String` 或数值类型。  
  
 下面是表达式的示例。  
  
 `5 + 4`  
  
 `' The preceding expression evaluates to 9.`  
  
 `15 * System.Math.Sqrt(9) + x`  
  
 `' The preceding expression evaluates to 45 plus the value of x.`  
  
 `"Concat" & "ena" & "tion"`  
  
 `' The preceding expression evaluates to "Concatenation".`  
  
 `763 < 23`  
  
 `' The preceding expression evaluates to False.`  
  
 几个运算符可以在一个表达式或语句中执行操作，如下面的示例所示：  
  
 [!code-vb[VbVbalrOperators#56](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/index_1.vb)]  
  
 在前面的示例中，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 在赋值运算符 \(`=`\) 右侧的表达式中执行运算，然后将结果值赋给左侧的变量 `x`。  对于可组合到表达式中的运算符的数量没有实际限制，但是需要理解 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md) 才能确保获得预期结果。  
  
 有关更多信息和示例，请参见 [Operator Overloading in Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703)（Visual Basic 2005 中的运算符重载）。  
  
## 请参阅  
 [运算符](../../../../visual-basic/language-reference/operators/index.md)   
 [运算符的有效组合](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)   
 [语句](../../../../visual-basic/language-reference/statements/index.md)