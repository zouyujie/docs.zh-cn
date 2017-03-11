---
title: "显式数值转换表（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "转换 [C#], 显式数值"
  - "显式数值转换 [C#]"
  - "数值转换 [C#], explicit"
  - "数值数据类型 [C#]"
  - "类型转换 [C#], 显式数值"
  - "类型 [C#], 显式数值转换"
ms.assetid: f3bb9e76-6b92-4df7-bc36-f866c24e1dfd
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# 显式数值转换表（C# 参考）
显式数值转换用于通过显式转换表达式，将任何数字类型转换为任何其他数字类型。对于它不存在隐式转换。  下表显示了这些转换。  
  
 有关转换的更多信息，请参见 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)。  
  
|发件人|若要|  
|---------|--------|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|`Sbyte` 或 `char`|  
|[short](../../../csharp/language-reference/keywords/short.md)|`sbyte`、`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|`sbyte`、`byte`、`short` 或 `char`|  
|[int](../../../csharp/language-reference/keywords/int.md)|`sbyte`、`byte`、`short`、`ushort`、`uint`、`ulong` 或 `char`|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|`sbyte`、`byte`、`short`、`ushort`、`int` 或 `char`|  
|[long](../../../csharp/language-reference/keywords/long.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`ulong` 或 `char`|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 或 `char`|  
|[char](../../../csharp/language-reference/keywords/char.md)|`sbyte`、`byte` 或 `short`|  
|[float](../../../csharp/language-reference/keywords/float.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char` 或 `decimal`|  
|[double](../../../csharp/language-reference/keywords/double.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `decimal`|  
|[decimal](../../../csharp/language-reference/keywords/decimal.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `double`|  
  
## 备注  
  
-   显式数值转换可能导致精度损失或引发异常。  
  
-   将 `decimal` 值转换为整型时，该值将舍入为与零最接近的整数值。  如果结果整数值超出目标类型的范围，则会引发 <xref:System.OverflowException>。  
  
-   将 `double` 或 `float` 值转换为整型时，值会被截断。  如果该结果整数值超出了目标值的范围，其结果将取决于溢出检查上下文。  在 checked 上下文中，将引发 `OverflowException`；而在 unchecked 上下文中，结果将是一个未指定的目标类型的值。  
  
-   将 `double` 转换为 `float` 时，`double` 值将舍入为最接近的 `float` 值。  如果 `double` 值因过小或过大而使目标类型无法容纳它，则结果将为零或无穷大。  
  
-   将 `float` 或 `double` 转换为 `decimal` 时，源值将转换为 `decimal` 表示形式，并舍入为第 28 个小数位之后最接近的数（如果需要）。  根据源值的不同，可能产生以下结果：  
  
    -   如果源值因过小而无法表示为 `decimal`，那么结果将为零。  
  
    -   如果源值为 NaN（非数字值）、无穷大或因过大而无法表示为 `decimal`，则会引发 `OverflowException`。  
  
-   将 `decimal` 转换为 `float` 或 `double` 时，`decimal` 值将舍入为最接近的 `double` 或 `float` 值。  
  
 有关显式转换的更多信息，请参见“C\# 语言规范中的显式”。  有关如何访问此规范的更多信息，请参见 [C\# 语言规范](../../../csharp/language-reference/language-specification.md)。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [\(\) 运算符](../../../csharp/language-reference/operators/invocation-operator.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)