---
title: "字符串和其他类型之间的转换 (Visual Basic) | Microsoft Docs"
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
  - "转换, 数据类型"
  - "转换, 类型"
  - "数据类型转换, string"
  - "区域选项"
  - "字符串转换"
  - "类型转换, string"
ms.assetid: c3a99596-f09a-44a5-81dd-1b89a094f1df
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 字符串和其他类型之间的转换 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

可以将数字、`Boolean` 或日期\/时间值转换为 `String`。  如果字符串的内容可以被解释为目标数据类型的有效值，则也可以反向转换，即从字符串值转换为数字、`Boolean` 或 `Date`。  如果无法转换，则出现运行时错误。  
  
 所有这些赋值在两个方向上的转换都是双字节到单字节转换。  应该使用类型转换关键字（`CBool`、`CByte`、`CDate`、`CDbl`、`CDec`、`CInt`、`CLng`、`CSByte`、`CShort`、`CSng`、`CStr`、`CUInt`、`CULng`、`CUShort` 和 `CType`）。  <xref:Microsoft.VisualBasic.Strings.Format%2A> 和 <xref:Microsoft.VisualBasic.Conversion.Val%2A> 函数提供了对字符串和数字间转换的额外控制。  
  
 如果您定义了类或结构，可以定义 `String` 与您的类或结构的类型之间的类型转换运算符。  有关更多信息，请参见 [如何：定义转换运算符](../Topic/How%20to:%20Define%20a%20Conversion%20Operator%20\(Visual%20Basic\).md)。  
  
## 数字到字符串的转换  
 可以使用 `Format` 函数将数字转换为格式化字符串，其中不仅可以包括相应的数字，而且可以包括格式化符号，例如货币符号（如 `$`）、千位分隔符或数字分组符号（如 `,`）以及小数分隔符（如 `.`）。  `Format` 根据 Windows**“控制面板”**中指定的**“区域选项”**设置自动使用相应的符号。  
  
 请注意，串联 \(`&`\) 运算符可以将数字隐式转换为字符串，如下例所示：  
  
```  
' The following statement converts count to a String value.  
Str = "The total count is " & count  
```  
  
## 字符串到数字的转换  
 可以使用 `Val` 函数将字符串中的数字显式转换为一个数字。  `Val` 读取字符串，直到遇到数字、空格、制表符、换行符或句号以外的字符。  “&O”和“&H”序列改变数字系统的基并终止扫描。  在停止读取之前，`Val` 将所有合适的字符转换为数值。  例如，下列语句返回值 `141.825`。  
  
 `Val("   14   1.825 miles")`  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 将字符串转换为数值时，它使用 Windows**“控制面板”**中指定的**“区域选项”**设置来解释千位分隔符、小数分隔符和货币符号。  这意味着在一种设置下可能成功的转换在另一种设置下不一定成功。  例如，`"$14.20"` 在英语（美国）区域设置中是可接受的，而在法语区域设置中则不接受。  
  
## 请参阅  
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [如何：在 Visual Basic 中将一个对象转换为其他类型](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [介绍基于 .NET Framework 的国际应用程序](/visual-studio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)