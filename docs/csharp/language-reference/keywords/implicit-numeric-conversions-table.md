---
title: "隐式数值转换表（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "转换 [C#], 隐式数值"
  - "隐式数值转换 [C#]"
  - "数值转换 [C#], implicit"
  - "类型 [C#], 隐式数值转换"
ms.assetid: 72eb5a94-0491-48bf-8032-d7ebfdfeb8d8
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# 隐式数值转换表（C# 参考）
下表显示了预定义的隐式数值转换。  隐式转换可能在多种情形下发生，包括调用方法时和在赋值语句中。  
  
|发件人|若要|  
|---------|--------|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|`short`、`int`、`long`、`float`、`double` 或 `decimal`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`float`、`double` 或 `decimal`|  
|[short](../../../csharp/language-reference/keywords/short.md)|`int`、`long`、`float`、`double` 或 `decimal`|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|`int`、`uint`、`long`、`ulong`、`float`、`double` 或 `decimal`|  
|[int](../../../csharp/language-reference/keywords/int.md)|`long`、`float`、`double` 或 `decimal`|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|`long`、`ulong`、`float`、`double` 或 `decimal`|  
|[long](../../../csharp/language-reference/keywords/long.md)|`float`、`double` 或 `decimal`|  
|[char](../../../csharp/language-reference/keywords/char.md)|`ushort`、`int`、`uint`、`long`、`ulong`、`float`、`double` 或 `decimal`|  
|[float](../../../csharp/language-reference/keywords/float.md)|`double`|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|`float`、`double` 或 `decimal`|  
  
## 备注  
  
-   可能从转换中丢失精度，但不是模`int`， `uint`， `long`，或`ulong`到`float`和`long`或`ulong`到`double`。  
  
-   不存在到 `char` 类型的隐式转换。  
  
-   不存在浮点型与 `decimal` 类型之间的隐式转换。  
  
-   `int` 类型的常数表达式可转换为 `sbyte`、`byte`、`short`、`ushort`、`uint` 或 `ulong`，前提是常数表达式的值处于目标类型的范围之内。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)   
 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)