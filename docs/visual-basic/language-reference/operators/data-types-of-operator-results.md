---
title: "运算符结果的数据类型 (Visual Basic) | Microsoft Docs"
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
  - "数据类型 [Visual Basic], 运算符结果数据类型"
  - "数据类型 [Visual Basic], 范围"
  - "运算符结果数据类型"
  - "运算符 [Visual Basic], 数据类型"
  - "运算符 [Visual Basic], 结果数据类型"
  - "结果数据类型"
ms.assetid: 9d524533-e1a1-4aa8-b1b8-622068173d06
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 运算符结果的数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 根据操作数的数据类型来确定运算的结果数据类型。  在某些情况下，该类型的范围可能要比两个操作数中任何一个的范围更大。  
  
## 数据类型范围  
 相关数据类型的范围按最小到最大的顺序显示如下：  
  
-   [Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md) — 两个可能的值  
  
-   [SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)、[Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md) — 256 个可能的整数值  
  
-   [Short](../../../visual-basic/language-reference/data-types/short-data-type.md)、[UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md) — 65,536 \(6.5...E\+4\) 个可能的整数值  
  
-   [Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)、[UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md) — 4,294,967,296 \(4.2...E\+9\) 个可能的整数值  
  
-   [Long](../../../visual-basic/language-reference/data-types/long-data-type.md), [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md) — 18,446,744,073,709,551,615 \(1.8...E\+19\) 个可能的整数值  
  
-   [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md) — 1.5...E\+29 个可能的整数值，最大范围 7.9...E\+28（绝对值）  
  
-   [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) — 最大范围 3.4...E\+38（绝对值）  
  
-   [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) — 最大范围 1.7...E\+308（绝对值）  
  
 有关 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 数据类型的更多信息，请参见 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
 如果操作数的计算结果为 [Nothing](../../../visual-basic/language-reference/nothing.md)，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 算术运算符将其视为零。  
  
## Decimal 算法  
 请注意，[Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md) 数据类型既不是浮点型也不是整型。  
  
 在 `+`、`–`、`*`、`/` 或 `Mod` 运算中，如果两个操作数中的一个是 `Decimal`，而另一个不是 `Single` 或 `Double`，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将另一个操作数扩展为 `Decimal`。  就是说，它以 `Decimal` 类型执行运算，结果数据类型为 `Decimal`。  
  
## 浮点算法  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 以 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) 类型执行大多数浮点算法，对浮点运算来说，这是最有效的数据类型。  但是，如果一个操作数为 [Single](../../../visual-basic/language-reference/data-types/single-data-type.md)，而另一个操作数不是 `Double`，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将以 `Single` 类型执行运算。  它在运算前根据需要将每个操作数扩展为相应的数据类型，运算结果也为该数据类型。  
  
### 运算符 \/ 和 ^  
 `/` 运算符仅为 [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)、[Single](../../../visual-basic/language-reference/data-types/single-data-type.md) 和 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) 数据类型而定义。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前根据需要将每个操作数扩展为相应的数据类型，运算结果也为该数据类型。  
  
 下表显示 `/` 运算符的结果数据类型。  请注意，此表是对称的；对于给定的操作数数据类型组合，无论操作数的顺序如何，结果数据类型都是相同的。  
  
||||||  
|-|-|-|-|-|  
||`Decimal`|`Single`|`Double`|任意整型|  
|`Decimal`|Decimal|Single|Double|Decimal|  
|`Single`|Single|Single|Double|Single|  
|`Double`|Double|Double|Double|Double|  
|任意整型|Decimal|Single|Double|Double|  
  
 `^` 运算符仅为 `Double` 数据类型而定义。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前根据需要将每个操作数扩展为 `Double`，运算结果的数据类型始终是 `Double`。  
  
## 整数算法  
 整型运算的结果数据类型取决于操作数的数据类型。  一般情况下，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 使用下面的策略确定结果数据类型：  
  
-   如果二元运算符的两个操作数具有相同的数据类型，则结果也为该数据类型。  例外的情况是 `Boolean`，该类型会被强制转换为 `Short` 类型。  
  
-   如果无符号操作数与有符号操作数一同参与运算，则结果将为有符号类型，其范围至少与两个操作数的数据类型范围中的一个相等。  
  
-   否则，结果数据类型的范围通常是两个操作数的数据类型中范围较大的一个。  
  
 请注意，结果数据类型可能不同于两个操作数的数据类型中的任何一个。  
  
> [!NOTE]
>  结果数据类型并不总是大得足以容纳运算产生的所有可能的值。  如果结果的值对其数据类型来说太大，则将引发 <xref:System.OverflowException> 异常。  
  
### 一元运算符 \+ 和 –  
 下表显示两个一元运算符 `+` 和 `–` 的结果数据类型。  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|一元 `+`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|一元 `–`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
  
### 运算符 \<\< 和 \>\>  
 下表显示两个移位运算符 `<<` 和 `>>` 的结果数据类型。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将每个移位运算符视为其左操作数（要移动的位模式）的一元运算符。  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`<<`, `>>`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 如果左操作数为 `Decimal`、`Single`、`Double` 或 `String`，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前会尝试将其转换为 `Long`，并且运算的结果数据类型为 `Long`。  右操作数（要移动的位的位置数）必须是 `Integer` 或扩展为 `Integer` 类型。  
  
### 二元运算符 \+、–、\* 和 Mod  
 下表显示二元运算符 `+`、`–`、`*` 和 `Mod` 的结果数据类型。  请注意，此表是对称的；对于给定的操作数数据类型组合，无论操作数的顺序如何，结果数据类型都是相同的。  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Decimal|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Decimal|  
|`ULong`|Decimal|Decimal|ULong|Decimal|ULong|Decimal|ULong|Decimal|ULong|  
  
### \\ 运算符  
 下表显示 `\` 运算符的结果数据类型。  请注意，此表是对称的；对于给定的操作数数据类型组合，无论操作数的顺序如何，结果数据类型都是相同的。  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 如果 `\` 运算符两个操作数中的任何一个为 [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)、[Single](../../../visual-basic/language-reference/data-types/single-data-type.md) 或 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前会尝试将其转换为 [Long](../../../visual-basic/language-reference/data-types/long-data-type.md)，并且运算的结果数据类型为 `Long`。  
  
## 关系比较和按位比较  
 关系运算（`=`、`<>`、`<`、`>`、`<=` 和 `>=`）的结果数据类型总是 `Boolean`[Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md)。  对于 `Boolean` 操作数的逻辑运算（`And`、`AndAlso`、`Not`、`Or`、`OrElse` 和 `Xor`），情况也是如此。  
  
 按位逻辑运算的结果数据类型取决于操作数的数据类型。  请注意，仅对 `Boolean` 定义 `AndAlso` 和 `OrElse`。[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前根据需要将每个操作数转换为 `Boolean`。  
  
### 运算符 \=、\<\>、\<、\>、\<\= 和 \>\=  
 如果两个操作数都为 `Boolean`，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 认为 `True` 小于 `False`。  如果将数字类型与 `String` 比较，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前会尝试将 `String` 转换为 `Double`。  `Char` 或 `Date` 操作数只能与同一数据类型的另一个操作数进行比较。  结果数据类型总是 `Boolean`。  
  
### 按位运算符 Not  
 下表显示按位运算符 `Not` 的结果数据类型。  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Not`|Boolean|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 如果操作数为 `Decimal`、`Single`、`Double` 或 `String`，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前会尝试将其转换为 `Long`，并且运算的结果数据类型为 `Long`。  
  
### 按位运算符 And、Or 和 Xor  
 下表显示按位运算符 `And`、`Or` 和 `Xor` 的结果数据类型。  请注意，此表是对称的；对于给定的操作数数据类型组合，无论操作数的顺序如何，结果数据类型都是相同的。  
  
|||||||||||  
|-|-|-|-|-|-|-|-|-|-|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Boolean|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 如果一个操作数为 `Decimal`、`Single`、`Double` 或 `String`，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前会尝试将其转换为 `Long`，并且运算的结果数据类型也为 `Long`。  
  
## 其他运算符  
 `&` 运算符仅为 `String` 操作数的串联而定义。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前根据需要将每个操作数转换为 `String`，运算的结果数据类型总是 `String`。  对 `&` 运算符来说，即使 `Option Strict` 为 `On`，也会将所有向 `String` 的转换视为扩展。  
  
 `Is` 和 `IsNot` 运算符要求两个操作数均为引用类型。  `TypeOf`...`Is` 表达式要求第一个操作数为引用类型，第二个操作数为数据类型的名称。  在以上所有情况下，结果数据类型都为 `Boolean`。  
  
 `Like` 运算符仅为 `String` 操作数的模式匹配而定义。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 在运算前会根据需要尝试将每个操作数转换为 `String`。  结果数据类型总是 `Boolean`。  
  
## 请参阅  
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [算术运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [比较运算符 \(Visual Basic\)](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [运算符](../../../visual-basic/language-reference/operators/index.md)   
 [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [比较运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)