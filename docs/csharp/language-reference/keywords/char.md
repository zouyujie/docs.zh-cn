---
title: "char（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "char"
  - "char_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "char 数据类型 [C#]"
ms.assetid: b51cf4fb-124c-4067-af48-afbac122b228
caps.latest.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 27
---
# char（C# 参考）
`char` 关键字用于声明 .NET framework 使用 Unicode 字符表示 <xref:System.Char?displayProperty=fullName> 结构的实例。  `Char` 对象的值是 16 位数字 \(序号值。\)  
  
 Unicode 字符在世界上表示大多数书面语言。  
  
|类型|范围|大小|.NET Framework 类型|  
|--------|--------|--------|-----------------------|  
|`char`|U\+0000 到 U\+FFFF|16 位 Unicode 字符|<xref:System.Char?displayProperty=fullName>|  
  
## 文本  
 `char` 类型的常数可以写成字符、十六进制换码序列或 Unicode 表示形式。  您也可以显式转换整数字符代码。  在下面的示例中，四个 `char` 变量使用同一字符 `X` 初始化：  
  
 [!code-cs[csrefKeywordsTypes#19](../../../csharp/language-reference/keywords/codesnippet/csharp/char_1.cs)]  
  
## 转换  
 `char` 可以隐式转换为 [ushort](../../../csharp/language-reference/keywords/ushort.md)、[int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md)。  但是，不存在从其他类型到 `char` 类型的隐式转换。  
  
 <xref:System.Char?displayProperty=fullName> 类型提供几个处理 `char` 值的静态方法。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Char>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)   
 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)