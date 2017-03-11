---
title: "如何：计算数值 (Visual Basic) | Microsoft Docs"
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
  - "计算, 数值表达式"
  - "表达式 [Visual Basic], 数值"
  - "数值表达式"
  - "运算符优先级"
  - "运算符 [Visual Basic]"
  - "优先级, 运算符"
  - "Visual Basic 代码, 表达式"
  - "Visual Basic 代码, 运算符"
ms.assetid: ba6bf43d-bd96-49b8-b1de-4a7797551372
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：计算数值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以通过使用数值表达式来计算数值。  “数值表达式”一种表达式，它包含表示数值的文本、常数和变量以及处理这些值的运算符。  
  
## 计算数值  
  
#### 计算数值  
  
-   将一个或多个数值文本、常数和变量合并为一个数值表达式。  下面的示例演示一些有效的数值表达式。  
  
     `93.217`  
  
     `System.Math.PI`  
  
     `counter`  
  
     `4 * (67 + i)`  
  
     前三行显示一个文本、一个常数以及一个变量。  每一行本身也组成一个有效的数值表达式。  最后一行显示一个变量和两个文本的组合。  
  
     请注意，数值表达式本身并未组成一个完整的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 语句。  您必须使用该表达式作为完整语句的一部分。  
  
#### 存储数值  
  
-   可以使用赋值语句将数值表达式代表的值赋给变量，如下面的示例所示。  
  
     [!code-vb[VbVbalrOperators#82](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-calculate-numeric_1.vb)]  
  
     在前面的示例中，等于运算符 \(`=`\) 右侧的表达式的值被赋给运算符左侧的变量 `j`，因此 `j` 的计算结果为 276。  
  
     有关更多信息，请参见 [语句](../../../../visual-basic/language-reference/statements/index.md)。  
  
## 多个运算符  
 如果数值表达式包含多个运算符，则它们的计算顺序由运算符优先级的规则确定。  若要重写运算符优先级的规则，请将表达式放在括号中，如上面的示例中所示；将会首先计算括号内的表达式。  
  
#### 重写常规运算符优先级  
  
-   使用括号括住您想要先执行的运算。  下面的示例显示了使用相同操作数和运算符计算得出的两个不同结果。  
  
     [!code-vb[VbVbalrOperators#83](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-calculate-numeric_2.vb)]  
  
     在前面的示例中，`j` 的计算将先执行加法运算符 \(`+`\)，原因是 `(67 + i)` 两边的括号重写了常规优先级，因此赋给 `j` 的值为 276（4 乘以 69）。  `k` 的计算将按常规优先级执行这些运算符（先执行 `*`，然后再执行 `+`），因此赋给 `k` 的值为 270（268 加 2）。  
  
     有关更多信息，请参见 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)。  
  
## 请参阅  
 [运算符和表达式](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [值的比较](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [语句](../../../../visual-basic/language-reference/statements/index.md)   
 [Visual Basic 中的运算符优先级](../../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [算术运算符](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [运算符的有效组合](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)