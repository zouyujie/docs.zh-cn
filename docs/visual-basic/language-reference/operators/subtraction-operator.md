---
title: "- 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Negate"
  - "vb.-"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "- 运算符 [Visual Basic]"
  - "算术运算符, 减法"
  - "差异运算符"
  - "数学运算符"
  - "减法运算符 [Visual Basic]"
  - "非运算符"
  - "运算符 [Visual Basic], 算法"
  - "运算符 [Visual Basic], 差异"
  - "运算符 [Visual Basic], 非"
  - "运算符 [Visual Basic], 减法"
  - "减法运算符, 语法"
ms.assetid: bff2c368-662d-4c92-ac87-1d9bdfd3426a
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# - 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

返回两个数值表达式之差或返回一个数值表达式的负值。  
  
## 语法  
  
```  
  
      expression1 – expression2  
- or -  
– expression1  
```  
  
## 部件  
 `expression1`  
 必选。  任何数值表达式。  
  
 `expression2`  
 必需（除非 `–` 运算符正在计算负值）。  任何数值表达式。  
  
## 结果  
 结果为 `expression1` 和 `expression2` 之差，或 `expression1` 的负值。  
  
 结果数据类型是适用于 `expression1` 和 `expression2` 的数据类型的数值类型。  请参见 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md) 中的“整数算法”表。  
  
## 支持的类型  
 所有数值类型。  这包括无符号类型和浮点类型以及 `Decimal`。  
  
## 备注  
 在上述语法中的第一个应用中，`–` 运算符为二进制算术减法运算符，用于计算两个数值表达式之差。  
  
 在上述语法中的第二个应用中，`–` 运算符为一元求反运算符，用于计算一个表达式的负值。  在这种情况下，求反运算将逆转 `expression1` 的符号，因此当 `expression1` 为负时，结果为正。  
  
 如果有一个表达式的计算结果为 [Nothing](../../../visual-basic/language-reference/nothing.md)，则 `–` 运算符将其视为零。  
  
> [!NOTE]
>  `–` 运算符可以被重载，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码对这样的类或结构使用此运算符，请确保您了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 下面的示例使用 `–` 运算符计算并返回两个数字之差，然后对一个数字进行求反运算。  
  
 [!code-vb[VbVbalrOperators#10](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/subtraction-operator_1.vb)]  
  
 执行这些语句之后，`binaryResult` 为 124.45，`unaryResult` 为 –334.90。  
  
## 请参阅  
 [\-\= 运算符](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)