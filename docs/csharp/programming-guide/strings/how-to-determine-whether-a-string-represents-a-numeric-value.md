---
title: "如何：确定字符串是否表示数值（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "数值字符串 [C#]"
  - "字符串 [C#], 数值"
  - "验证数字输入 [C#]"
ms.assetid: a4e84e10-ea0a-489f-a868-503dded9d85f
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# 如何：确定字符串是否表示数值（C# 编程指南）
若要确定字符串是否是指定数值类型的有效表示形式，请使用静态的 `TryParse` 方法，该方法由所有基元数值类型以及诸如 <xref:System.DateTime> 和 <xref:System.Net.IPAddress> 这样的类型实现。  下面的示例演示如何确定“108”是否为有效的 [int](../../../csharp/language-reference/keywords/int.md) 类型。  
  
```  
int i = 0;   
string s = "108";  
bool result = int.TryParse(s, out i); //i now = 108  
```  
  
 如果字符串包含非数值字符或者所包含的数值对于指定的特定类型而言太大或太小，`TryParse` 都将返回 false 并将 out 参数设置为零。  否则，它将返回 true，并且将 out 参数设置为字符串的数值。  
  
> [!NOTE]
>  有时，虽然字符串可能只包含数值字符，对于您使用的 `TryParse` 方法所属的类型却仍然会无效。  例如，“256”对于 `byte` 类型不是有效值，但对于 `int` 类型有效。"  98.6”对于 `int` 类型不是有效值，但对于 `decimal` 类型有效。  
  
## 示例  
 下面的示例演示如何对 `long`、`byte` 和 `decimal` 值的字符串表示形式使用 `TryParse`。  
  
 [!code-cs[csProgGuideStrings#14](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#14)]  
  
## 可靠编程  
 基元数值类型还实现了 `Parse` 静态方法，此方法会在字符串不是有效数字时引发异常。  `TryParse` 通常更加有效，因为它在数字无效时只是返回 false。  
  
## .NET Framework 安全性  
 请始终使用 `TryParse` 或 `Parse` 方法来验证用户在文本框和组合框等控件中输入的内容。  
  
## 请参阅  
 [如何：将字节数组转换为 int](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md)   
 [如何：将字符串转换为数字](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)   
 [如何：在十六进制字符串与数值类型之间转换](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)   
 [分析数值字符串](../Topic/Parsing%20Numeric%20Strings%20in%20the%20.NET%20Framework.md)   
 [格式化类型](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md)