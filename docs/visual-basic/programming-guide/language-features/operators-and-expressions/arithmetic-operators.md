---
title: "算术运算符 (Visual Basic) | Microsoft Docs"
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
  - "算术运算符, 关于算术运算符"
  - "移位运算符"
  - "按位运算符"
  - "除法, 被零除"
  - "运算符 [Visual Basic], 算法"
  - "运算符 [Visual Basic], 移位"
  - "运算符 [Visual Basic], 按位"
  - "类型安全"
  - "Visual Basic 代码, 运算符"
  - "零, 被零除"
ms.assetid: 325dac7a-ea4f-41d5-8b48-f6e904211569
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 算术运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

算术运算符用于执行很多熟悉的算术运算，涉及计算由文本、变量、其他表达式、函数和属性调用以及常数表示的数值。  另外，移位运算符也属于算术运算符，它们在操作数的单个位级别起作用，并将操作数的位模式向左或向右移。  
  
## 算术运算  
 可以使用 [\+ 运算符](../../../../visual-basic/language-reference/operators/addition-operator.md) 将表达式中的两个值加在一起，或者使用 [\- 运算符](../../../../visual-basic/language-reference/operators/subtraction-operator.md) 从一个值中减去另一个值，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators#57](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_1.vb)]  
  
 求反也使用 [\- 运算符](../../../../visual-basic/language-reference/operators/subtraction-operator.md)，但只带一个操作数，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators#58](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_2.vb)]  
  
 乘法和除法分别使用 [\* 运算符](../../../../visual-basic/language-reference/operators/multiplication-operator.md) 和 [\/ 运算符](../../../../visual-basic/language-reference/operators/floating-point-division-operator.md)，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators#59](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_3.vb)]  
  
 求幂使用 [^ 运算符](../../../../visual-basic/language-reference/operators/exponentiation-operator.md)，如下面的示例所示。  
  
 [!code-vb[VbVbalrOperators#60](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_4.vb)]  
  
 使用 [\\ 运算符](../../../../visual-basic/language-reference/operators/integer-division-operator.md) 执行整除。  整除会返回商数，它是一个整数，表示在不考虑有余数的情况下，除数可以除被除数的次数。  对此运算符来说，除数和被除数必须为整型（`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long` 和 `ULong`）。  所有其他类型都必须首先转换为整型。  下面的示例演示如何进行整除。  
  
 [!code-vb[VbVbalrOperators#61](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_5.vb)]  
  
 使用 [Mod 运算符](../../../../visual-basic/language-reference/operators/mod-operator.md) 执行求模算法。  此运算符返回除数除被除数整数次后的余数。  如果除数和被除数都是整型，则返回值是整数。  如果除数和被除数都是浮点型，则返回值也是浮点型。  下面的示例演示这一行为。  
  
 [!code-vb[VbVbalrOperators#62](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_6.vb)]  
  
 [!code-vb[VbVbalrOperators#63](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_7.vb)]  
  
### 尝试用零作除数  
 根据所涉及的数据类型，被零除会得到不同的结果。  在整除中（`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`），[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 将引发 <xref:System.DivideByZeroException> 异常。  在对 `Decimal` 或 `Single` 数据类型执行的除法运算中，[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 也将引发 <xref:System.DivideByZeroException> 异常。  
  
 在涉及 `Double` 数据类型的浮点除法运算中，不会引发异常，运算结果为表示 <xref:System.Double.NaN>、<xref:System.Double.PositiveInfinity> 或 <xref:System.Double.NegativeInfinity> 的类成员，具体取决于被除数。  下表汇总了尝试用零除 `Double` 值所得的各种结果。  
  
|||||  
|-|-|-|-|  
|被除数数据类型|除数数据类型|被除数的值|结果|  
|`Double`|`Double`|0|<xref:System.Double.NaN>（不是数学定义的数字）|  
|`Double`|`Double`|\> 0|<xref:System.Double.PositiveInfinity>|  
|`Double`|`Double`|\< 0|<xref:System.Double.NegativeInfinity>|  
  
 当捕获 <xref:System.DivideByZeroException> 异常时，可使用其成员帮助处理该异常。  例如，<xref:System.Exception.Message%2A> 属性保留了该异常的消息文本。  有关更多信息，请参见 [Try...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## 移位运算  
 移位运算对位模式进行数学移位。  模式包含在左侧的操作数中，而右侧的操作数指定要对该模式移位的位数。  可以使用 [\>\> 运算符](../../../../visual-basic/language-reference/operators/right-shift-operator.md) 将该模式向右移，或者使用 [\<\< 运算符](../Topic/%3C%3C%20Operator%20\(Visual%20Basic\).md) 向左移。  
  
 模式操作数的数据类型必须为 `SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long` 或 `ULong`。  表示移位位数的操作数数据类型必须为 `Integer`，或者必须扩大到 `Integer`。  
  
 数学移位不是循环的，即不会将在结果的一端移出的数位从另一端重新移入。  移位操作空出的数位位置按以下方式设置：  
  
-   进行数学左移位时，设置为 0  
  
-   对正数进行数学右移位时，设置为 0  
  
-   对负数据类型（`Byte`、`UShort`、`UInteger`、`ULong`）进行数学右移位时，设置为 0  
  
-   对正数（`SByte`、`Short`、`Integer` 或 `Long`）进行数学右移位时，设置为 1  
  
 下面的示例对 `Integer` 值进行左移和右移。  
  
 [!code-vb[VbVbalrOperators#64](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/arithmetic-operators_8.vb)]  
  
 数学移位绝不会产生溢出异常。  
  
## 按位运算  
 `Not`、`Or`、`And` 和 `Xor` 除了作为逻辑运算符之外，当用于数值时，还可执行按位算术运算。  有关更多信息，请参见 [Visual Basic 中的逻辑运算符和位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md) 中的“按位运算”。  
  
## 类型安全  
 操作数通常应为同一类型。  例如，如果在对 `Integer` 变量进行加法运算，与它相加的变量应为 `Integer`，运算结果也应赋给 `Integer` 类型的变量。  
  
 确保采用良好类型安全编码的一种方法是使用 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)。  如果设置 `Option Strict On`，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将自动执行“类型安全”转换。  例如，如果尝试将 `Integer` 变量与 `Double` 变量相加，并将结果值赋给 `Double` 变量，运算将正常进行，因为 `Integer` 值可以转换为 `Double` 而不会损失任何数据。  另一方面，类型不安全的转换在 `Option Strict On` 时将导致编译器错误。  例如，如果尝试将 `Integer` 变量与 `Double` 变量相加，并将结果值赋给 `Integer` 变量，则会导致编译器错误，因为 `Double` 变量无法隐式转换为 `Integer` 类型。  
  
 不过，如果设置 `Option Strict Off`，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 则允许执行隐式缩小转换，尽管这样可能导致意外的数据或精度损失。  为此，我们建议在编写生产代码时使用 `Option Strict On`。  有关更多信息，请参见[扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
## 请参阅  
 [算术运算符](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [移位运算符](../../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [比较运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [串联运算符 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [运算符的有效组合](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)