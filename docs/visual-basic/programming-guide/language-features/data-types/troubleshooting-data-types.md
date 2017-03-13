---
title: "数据类型疑难解答 (Visual Basic) | Microsoft Docs"
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
  - "Boolean 数据类型, 转换"
  - "Char 数据类型, 转换"
  - "数据类型 [Visual Basic], 疑难解答"
  - "Decimal 数据类型, 转换"
  - "浮点数字"
  - "浮点数字, 比较"
  - "浮点数字, 不精确"
  - "浮点数字, 精度"
  - "文本类型的字符"
  - "文本类型"
  - "文本, 默认类型"
  - "Mod 运算符 [Visual Basic], 在浮点操作中"
  - "String 数据类型, 转换"
  - "数据类型疑难解答"
  - "Visual Basic 疑难解答, 数据类型"
  - "类型字符, 文本"
ms.assetid: 90040d67-b630-4125-a6ae-37195b079042
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# 数据类型疑难解答 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本页列出可能出现的常见问题，可以在对内部数据类型时的操作。  
  
## 浮点表达式的比较结果不相等  
 在使用浮点数 \([Single 数据类型](../../../../visual-basic/language-reference/data-types/single-data-type.md) 和 [Double 数据类型](../../../../visual-basic/language-reference/data-types/double-data-type.md)\)，请确保其存储为二进制分数。  这意味着它们不能保存不是二进制分数任意数量的精确表示 k 和 n 是整数 \(\) 的窗体 k \/ \(2 ^ n\) 。  例如， 0.5 \(\= 1\/2\) 和 0.3125 \(\= 5\/16\) 可保存为精确值，，而 0.2 \(\= 1\/5\) 和 0.3 \(\= 3\/10\) 可以是近似值。  
  
 因此，当您处理浮点值时，不精确性，不能依赖准确的结果。  具体而言，理论上相等的两个值具有略微不同的表示形式。  
  
||  
|-|  
|比较浮点数量|  
|1.  使用 <xref:System.Math> 类的 <xref:System.Math.Abs%2A> 方法在 <xref:System> 命名空间，计算它们之间的差值的绝对值。<br />2.  确定可接受的最大差异，这样可以将两个数实际上是相等的。，如果它们之间的差异没有更大。<br />3.  使用可接受的差值比较该差值的绝对值。|  
  
 下面的示例演示两个 `Double` 值的正确和错误的比较。  
  
 [!code-vb[VbVbalrDataTypes#10](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_1.vb)]  
  
 上面的示例使用 <xref:System.Double> 结构的 <xref:System.Double.ToString%2A> 方法，使其比 `CStr` 使用关键字时可以指定更高的精度。  默认值为 15 位数，，但 “G17”格式将其扩展到 17 位数字。  
  
## Mod 运算符未返回准确的结果  
 由于浮点存储的不精确性，如果至少一个 [Mod 运算符](../../../../visual-basic/language-reference/operators/mod-operator.md) 浮点操作数，时，可能会返回意外的结果。  
  
 [Decimal 数据类型](../../../../visual-basic/language-reference/data-types/decimal-data-type.md) 不使用浮点表示形式。  不精确在 `Single` 和 `Double` 的许多数字为确切在 `Decimal` \(如 0.2 和 0.3\)。  虽然算术运算速度上比 `Decimal` 在浮点，它可能会降低性能获得更高的精度。  
  
||  
|-|  
|找出浮点数量的整数余数|  
|1.  变量声明为 `Decimal`。<br />2.  但是，如果它们的值。 `Long` 数据类型来说太大，使用该文本类型字符 `D` 将文本强制为 `Decimal`。|  
  
 下面的示例演示了浮点操作数潜在的不精确性。  
  
 [!code-vb[VbVbalrDataTypes#11](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_2.vb)]  
  
 上面的示例使用 <xref:System.Double> 结构的 <xref:System.Double.ToString%2A> 方法，使其比 `CStr` 使用关键字时可以指定更高的精度。  默认值为 15 位数，，但 “G17”格式将其扩展到 17 位数字。  
  
 由于 `zeroPointTwo` 是 `Double`，其 0.2 的值是一个无限重复与中存储的值的二进制分数为 0.20000000000000001。  将 2.0 除以此数量将得到 9.9999999999999995 余数为 0.19999999999999991。  
  
 在 `decimalRemainder`的表达式，文本类型字符 `D` 将两个操作数均强制转换为 `Decimal`，并且， 0.2 将具有精确的表示形式。  因此 `Mod` 运算符将得到的余数 0.0。  
  
 请注意声明 `decimalRemainder` 作为 `Decimal`是不够的。  您还必须将文本强制为 `Decimal`，也使用 `Double` 默认情况下，它的 `decimalRemainder` 采用不正确的值和 `doubleRemainder`相同。  
  
## boolean 类型不能准确地转换为数值类型  
 [Boolean 数据类型](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) 值是存储为数字，因此，存储的值也不用等效于数字。  为了与早期版本兼容， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供转换关键字 \([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)， `CBool`， `CInt`，等等\) 将 `Boolean` 和 numeric 类型之间。  但是，其他语言有时会以不同的方式执行这些转换，如 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 方法。  
  
 绝不应依赖于 `True` 和 `False`的等效数字值的代码。  只要有可能，应为它们设计的逻辑值限制 `Boolean` 变量用法。  如果必须组合 `Boolean` 和数值，请确保您了解您选择的转换方法。  
  
### 在 Visual Basic 中的转换  
 当您使用 `CType` 或 `CBool` 转换关键字将数值数据类型转换为 `Boolean`时， 0 成为 `False` ，而所有其他值将成为 `True`。  通过使用转换关键字时，如果转换 `Boolean` 值转换为数值类型， `False` 变为 0，并 `True` 会变为 \-1。  
  
### 框架中的转换  
 <xref:System.Convert> 类的 <xref:System.Convert.ToInt32%2A> 方法在 <xref:System> 命名空间的转换 `True` 为 \+1。  
  
 如果必须将 `Boolean` 值转换为数值数据类型，请注意所使用的转换方法。  
  
## 字符文本产生编译器错误  
 如果没有任何类型字符时， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 假定文本使用默认数据类型。  字符文本的默认类型 —将括在引号 \(`" "`\) —是 `String`。  
  
 `String` 数据类型不 [Char 数据类型](../../../../visual-basic/language-reference/data-types/char-data-type.md)会扩大到。  这意味着，如果要分配文本到 `Char` 变量，则必须进行收缩转换或将文本强制 `Char` 类型。  
  
||  
|-|  
|创建一个字符文本分配给变量或常数|  
|1.  声明变量或常数作为 `Char`。<br />2.  将字符值用双引号 \(`" "`\)。<br />3.  遵循结束双引号与该文本类型字符 `C` 强制该文本到 `Char`。  这是所需的类型检查开关 \([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) 为 `On`，无论如何，非常适合的。|  
  
 下面的示例演示 `Char` 变量演示文本的操作和不成功的赋值操作。  
  
 [!CODE [VbVbalrStatements#49](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrStatements#49)]  
  
 [!code-vb[VbVbalrDataTypes#12](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/troubleshooting-data-types_3.vb)]  
  
 始终有使用收缩转换的一种风险，，因为它们可能会在运行时。  例如，因此，如果 `String` 值包含多个字符，从 `String` 的转换到 `Char` 会失败。  因此，它是使用 `C` 类型的更好的编程字符。  
  
## 字符串转换在运行时失败  
 [String 数据类型](../../../../visual-basic/language-reference/data-types/string-data-type.md) 参与非常少的扩大转换。  `String` 只扩大到自身和 `Object`，因此，仅 `Char` 和 `Char()` \( `Char` 数组\) 扩大到 `String`。  这是因为， `String` 变量和常数可以包含其他数据类型不能包含的值。  
  
 在类型检查开关 \([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) 为时 `On`，编译器不允许任何隐式收缩转换。  这包括涉及 `String`的功能。  您的代码仍可以使用转换关键字例如 `CStr` 和 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)，处理 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 尝试进行转换。  
  
> [!NOTE]
>  收缩转换错误为从元素的转换禁止在 `For Each…Next` 收集到循环控制变量。  有关更多信息和示例，请参见 “收缩转换” [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)一节。  
  
### 收缩转换保护  
 收缩转换的缺点是它们可能会在运行时。  例如，除 “true”或 “false " 以外，因此，如果 `String` 变量包含任何内容，则无法转换为 `Boolean`。  如果它包含标点符号，为任何数值类型的转换失败。  除非您知道您的 `String` 变量始终表示目标类型可以接受的值，则不应尝试进行转换。  
  
 如果必须从 `String` 转换为另一种数据类型，则最安全的做法是将尝试的转换 [Try...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  这使您能处理运行时失败。  
  
### 字符数组  
 唯一 `Char` 和数组 `Char` 元素两个扩大到 `String`。  但是， `String` 不会扩大到 `Char()`。  若要将 `String` 值转换为 `Char` 数组，可以使用 <xref:System.String?displayProperty=fullName> 类的 <xref:System.String.ToCharArray%2A> 方法。  
  
### 无意义的值  
 通常， `String` 值并没有意义在其他数据类型，因此，转换是人工和高度危险的。  只要有可能，应为它们设计的字符序列限制 `String` 变量用法。  绝不应依赖其他类型的等效值编写代码。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [类型字符](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [有效使用数据类型](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)