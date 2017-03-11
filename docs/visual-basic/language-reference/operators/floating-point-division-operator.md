---
title: "/ 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb./"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/ 运算符 [Visual Basic]"
  - "算术运算符, 除法"
  - "除法运算符, 浮点"
  - "除法运算符, 语法"
  - "除法, 被零除"
  - "浮点数字, 除法运算符"
  - "数学运算符"
  - "运算符 [Visual Basic], 算法"
  - "运算符 [Visual Basic], 除法"
  - "斜杠 (/) 运算符"
  - "零, 被零除"
ms.assetid: 335e97f2-c434-439e-9064-76973a051101
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# / 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将两个数相除并返回以浮点数表示的结果。  
  
## 语法  
  
```  
  
expression1 / expression2  
```  
  
## 部件  
 `expression1`  
 必选。  任何数值表达式。  
  
 `expression2`  
 必选。  任何数值表达式。  
  
## 支持的类型  
 所有数值类型，包括无符号和浮点类型以及 `Decimal`。  
  
## 结果  
 结果是 `expression1` 除以 `expression2` 的完整的商，包括任何余数。  
  
 [\\ 运算符](../../../visual-basic/language-reference/operators/integer-division-operator.md) 返回整数商，丢掉了余数。  
  
## 备注  
 所得结果的数据类型取决于操作数的类型。  下表显示如何确定结果的数据类型。  
  
|操作数数据类型|结果数据类型|  
|-------------|------------|  
|两个表达式都是整数数据类型（[SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)、[Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md)、[Short](../../../visual-basic/language-reference/data-types/short-data-type.md)、[UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)、[Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)、[UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)、[Long](../../../visual-basic/language-reference/data-types/long-data-type.md)、[ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)）|`Double`|  
|一个表达式为 [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) 数据类型，而另一个表达式不为 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Single`|  
|一个表达式为 [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md) 数据类型，而另一个表达式不为 [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) 或 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Decimal`|  
|任一表达式为 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) 数据类型|`Double`|  
  
 执行除法之前，任何整数数值表达式都会被扩展为 `Double`。  如果将结果赋给整数数据类型，Visual Basic 会尝试将结果从 `Double` 转换成这种类型。  如果结果不适合该类型，会引发异常。  有关详细信息，请参见本帮助页上的“尝试用零作除数”。  
  
 如果 `expression1` 或 `expression2` 计算结果等于 [Nothing](../../../visual-basic/language-reference/nothing.md)，则将其视为零。  
  
## 尝试用零作除数  
 如果 `expression2` 的计算结果等于零，则操作数数据类型不同，`/` 运算符的行为也不同。  下表显示可能的行为。  
  
|操作数数据类型|`expression2` 为零时的行为|  
|-------------|--------------------------|  
|浮点（`Single` 或 `Double`）|如果 `expression1` 也为零，则返回无穷（<xref:System.Double.PositiveInfinity> 或 <xref:System.Double.NegativeInfinity>）或 <xref:System.Double.NaN>（不是数字）|  
|`Decimal`|引发 <xref:System.DivideByZeroException>|  
|整数（有符号或无符号）|尝试转换回整型将引发 <xref:System.OverflowException>，因为整型不接受 <xref:System.Double.PositiveInfinity>、<xref:System.Double.NegativeInfinity> 或 <xref:System.Double.NaN>|  
  
> [!NOTE]
>  `/` 运算符可以被“重载”，这意味着当操作数具有某个类或结构的类型时，该类或结构可以重新定义其行为。  如果代码在这样的类或结构上使用此运算符，那么您一定要了解其重新定义的行为。  有关更多信息，请参见 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## 示例  
 本示例使用 `/` 运算符执行浮点除法。  结果是两个操作数的商。  
  
 [!code-vb[VbVbalrOperators#16](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/floating-point-division-_1_1.vb)]  
  
 前面的示例中的表达式返回值 2.5 和 3.333333。  请注意，即使两个操作数都是整数常数，结果也始终为浮点类型 \(`Double`\)。  
  
## 请参阅  
 [\/\= 运算符](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\\ 运算符](../../../visual-basic/language-reference/operators/integer-division-operator.md)   
 [运算符结果的数据类型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)