---
title: "如何：在十六进制字符串与数值类型之间转换（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "转换 [C#], 十六进制字符串"
  - "十六进制字符串 [C#]"
  - "十六进制字符串 [C#], 转换为数值类型"
  - "字符串 [C#], 转换十六进制字符串"
ms.assetid: 7115c49f-7d1d-40c3-8bd9-aae0cc1d46b6
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# 如何：在十六进制字符串与数值类型之间转换（C# 编程指南）
以下示例演示如何执行下列任务：  
  
-   获取[字符串](../../../csharp/language-reference/keywords/string.md)中每个字符的十六进制值。  
  
-   获取与十六进制字符串中的每个值对应的[字符](../../../csharp/language-reference/keywords/char.md)。  
  
-   将十六进制 `string` 转换为[整型](../../../csharp/language-reference/keywords/int.md)。  
  
-   将十六进制 `string` 转换为[浮点型](../../../csharp/language-reference/keywords/float.md)。  
  
-   将[字节](../../../csharp/language-reference/keywords/byte.md)数组转换为十六进制 `string`。  
  
## 示例  
 此示例输出 `string` 中的每个字符的十六进制值。  首先，它将 `string` 分析为字符数组，  然后对每个字符调用 <xref:System.Convert.ToInt32%28System.Char%29> 以获取相应的数字值。  最后，在 `string` 中将数字的格式设置为十六进制表示形式。  
  
 [!code-cs[csProgGuideTypes#30](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_1.cs)]  
  
## 示例  
 此示例分析十六进制值的 `string` 并输出对应于每个十六进制值的字符。  首先，它调用 [Split\(Char\<xref:System.String.Split%28System.Char%5B%5D%29> 方法以获取每个十六进制值作为数组中的单个 `string`。  然后调用 <xref:System.Convert.ToInt32%28System.String%2CSystem.Int32%29> 以将十六进制转换为表示为 [int](../../../csharp/language-reference/keywords/int.md) 的十进制值。  示例中演示了用于获取对应于该字符代码的字符的两种不同方法。  第一种方法是使用 <xref:System.Char.ConvertFromUtf32%28System.Int32%29>，它将对应于整型参数的字符作为 `string` 返回。  第二种方法是将 `int` 显式转换为 [char](../../../csharp/language-reference/keywords/char.md)。  
  
 [!code-cs[csProgGuideTypes#31](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_2.cs)]  
  
## 示例  
 此示例演示了将十六进制 `string` 转换为整数的另一种方法，即调用 <xref:System.Int32.Parse%28System.String%2CSystem.Globalization.NumberStyles%29> 方法。  
  
 [!code-cs[csProgGuideTypes#32](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_3.cs)]  
  
## 示例  
 下面的示例演示如何使用 <xref:System.BitConverter?displayProperty=fullName> 类和 <xref:System.Int32.Parse%2A?displayProperty=fullName> 方法将十六进制 `string` 转换为[浮点型](../../../csharp/language-reference/keywords/float.md)。  
  
 [!code-cs[csProgGuideTypes#39](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_4.cs)]  
  
## 示例  
 下面的示例演示如何使用 <xref:System.BitConverter?displayProperty=fullName> 类将[字节](../../../csharp/language-reference/keywords/byte.md)数组转换为十六进制字符串。  
  
 [!code-cs[csProgGuideTypes#38](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-between-hexadecimal-strings-and-numeric-types_5.cs)]  
  
## 请参阅  
 [标准数字格式字符串](../Topic/Standard%20Numeric%20Format%20Strings.md)   
 [类型](../../../csharp/programming-guide/types/index.md)   
 [如何：确定字符串是否表示数值](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)