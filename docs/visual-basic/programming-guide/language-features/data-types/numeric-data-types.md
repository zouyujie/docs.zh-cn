---
title: "数值型数据类型 (Visual Basic) | Microsoft Docs"
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
  - "数据类型 [Visual Basic], 数值"
  - "Decimal 数据类型, 数值型数据类型"
  - "Double 数据类型, 数值型数据类型"
  - "指数, 小数数字"
  - "小数数据类型"
  - "小数"
  - "Integer 数据类型, 数值型数据类型"
  - "整数数字"
  - "整数"
  - "整型, Visual Basic"
  - "Long 数据类型, Visual Basic 数值型数据类型"
  - "尾数"
  - "尾数, 小数数字"
  - "数字"
  - "数字, integer"
  - "数字, 整个"
  - "数值型数据类型, Visual Basic"
  - "Short 数据类型, 数值型数据类型"
  - "Single 数据类型, 数值类型"
  - "整数"
ms.assetid: a27bd4d0-7e14-43eb-9cc4-b42eaab323c9
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# 数值型数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供处理的数字多个 *数值数据类型* 在各种表示。  整型仅表示整数 \(正数，、负数和零\)，， " *非* 整型 " 带有整数部分和小数部分的表示数字。  
  
 有关演示 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 数据类型的并行比较的列表，请参见 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)。  
  
## 整型数值类型  
 整型*数据类型* " 是只表示数字，而没有小数部分\) 的。  
  
 带符号整型数据类型有 [SByte 数据类型](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md) \(8 位\)， [Short 数据类型](../../../../visual-basic/language-reference/data-types/short-data-type.md) \(16 位\)， [Integer 数据类型](../../../../visual-basic/language-reference/data-types/integer-data-type.md) \(32 位\)， [Long 数据类型](../../../../visual-basic/language-reference/data-types/long-data-type.md) \(64 位\)。  如果变量总是存储整数而不是小数，则将其声明为这些类型之一。  
  
 *无符号* 整数类型有 [Byte 数据类型](../../../../visual-basic/language-reference/data-types/byte-data-type.md) \(8 位\)， [Ushort 数据类型](../../../../visual-basic/language-reference/data-types/ushort-data-type.md) \(16 位\)， [UInteger 数据类型](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md) \(32 位\)， [Ulong 数据类型](../../../../visual-basic/language-reference/data-types/ulong-data-type.md) \(64 位\)。  如果变量包含二进制数据或未知种类的数据，则将其声明为这些类型之一。  
  
### 性能  
 算术运算速度快使用整型速度比其他数据类型。  它们是最快的 `Integer` ，并 `UInteger` 输入 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]。  
  
### 大整数  
 如果大于 `Integer` 数据类型所能存储的需要对整数负数，可以使用 `Long` 数据类型。  `Long` 变量可保存从 \-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 的数字。  与 `Long` 的操作比稍微慢一些 `Integer`。  
  
 如果需要更大的值，可以使用 [Decimal 数据类型](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)。  ，如果不使用任何小数位数，可以保存从 \-79,228,162,514,264,337,593,543,950,335 到 79,228,162,514,264,337,593,543,950,335 的数字在 `Decimal` 变量。  但是，与 `Decimal` 数字的运算速度比其他数值数据类型慢得多。  
  
### 小整数  
 如果不需要完整范围 `Integer` 数据类型，则可以使用 `Short` 数据类型，它可以保存整数 \-32,768 到 32,767\)。  最小整数范围， `SByte` 数据类型来保存整数 \-128 到 127\)。  如果您有一个小整数的一个非常大数量的变量，公共语言运行时有时可以更加高效地存储您的 `Short` 和 `SByte` 变量以节省内存使用。  但是，与 `Short` 的操作和 `SByte` 比稍慢一些 `Integer`。  
  
### 无符号整数  
 如果您知道您的变量永远不需要存储负数，可以使用 *无符号类型*`Byte`、 `UShort`、 `UInteger`和 `ULong`。  这些数据类型所能两次对一个正整数是相应的有符号类型 \(`SByte`、 `Short`、 `Integer`和 `Long`\)。  就性能而言，每个无符号类型正确的效率一样。相应的有符号类型。  具体而言， `UInteger` 与都是最有效的所有基本数值数据类型的 `Integer` 共享。  
  
## 非整型数值类型  
 *非整型数据类型* 是带有整数部分和小数部分的表示数字的项。  
  
 非整型数值数据类型是 `Decimal` \(128 位定点数\)， [Single 数据类型](../../../../visual-basic/language-reference/data-types/single-data-type.md) \(32 位浮点\)， [Double 数据类型](../../../../visual-basic/language-reference/data-types/double-data-type.md) \(64 位浮点\)。  它们都是有符号类型。  如果变量可以包含小数，则将其声明为这些类型之一。  
  
 `Decimal` 不是浮点数据类型。  `Decimal` 数字具有一个二进制整数值和指定的整数比例因子该值的哪些部分是小数部分。  
  
 可以为货币值使用 `Decimal` 变量。  其优点是值的精度。  `Double` 数据类型速度更快所需内存更少，但是，它会导致四舍五入错误。  `Decimal` 数据类型保留完全准确度。 28 个小数位。  
  
 浮点 \(`Single` 和 `Double`\) 是一 `Decimal` 数字具有更大的范围，但可能会导致四舍五入错误。  浮点类型与 `Decimal` 支持的有效数字，但它可以表示更大的值。  
  
 非整型数值可以表示为 mmmEeee， mmm 是 *尾数* " \(有效位数\)，并 eee 是 *指数* \(10 的次幂\)。  非整数类型的最大正值为 `Decimal`的 `Single`的 7.9228162514264337593543950335E\+28， `Double`的 3.4028235E\+38 和 1.79769313486231570E\+308。  
  
### 性能  
 ，因为当前平台上的处理器以双精度，执行浮点运算`Double` 是最有效的数据类型。  但是，与 `Double` 的操作相同的速度不象使用整型例如 `Integer`。  
  
### 小量值  
 对于具有最小可能的数字 \(最接近 0\)， `Double` 变量可以存储最小类似于负值的正值的 \-4.94065645841246544E\-324 和最大 4.94065645841246544E\-324。  
  
### 小的分数  
 如果不需要完整范围 `Double` 数据类型，则可以使用 `Single` 数据类型，它包含从 \-3.4028235E\+38 到 3.4028235e\+38 的浮点数。  `Single` 变量的最小量值为负值的正值的 \-1.401298E\-45 和 1.401298E\-45。  如果您有一个小浮点数的一个非常大数量的变量，公共语言运行时有时可以更加高效地存储您的 `Single` 变量以节省内存使用。  
  
## 请参阅  
 [基本数据类型](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [字符数据类型](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [其他数据类型](../../../../visual-basic/programming-guide/language-features/data-types/miscellaneous-data-types.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [如何：调用采用无符号类型的 Windows 函数](../../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)