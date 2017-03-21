---
title: "decimal（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "decimal_CSharpKeyword"
  - "decimal"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "decimal 关键字 [C#]"
ms.assetid: b6522132-b5ee-4be3-ad13-3adfdb7de7a1
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 32
---
# decimal（C# 参考）
`decimal` 关键字指示 128 位数据类型。  与浮点型相比，`decimal` 类型具有更高的精度和更小的范围，这使它适合于财务和货币计算。  `decimal` 类型的大致范围和精度如下表所示。  
  
|类型|大致范围|精度|.NET Framework 类型|  
|--------|----------|--------|-----------------------|  
|`decimal`|\(\-7.9 x 10<sup>28</sup> \- 7.9 x 10<sup>28</sup>\) \/ \(10<sup>0 - 28</sup>\)|28\-29 个有效位|<xref:System.Decimal?displayProperty=fullName>|  
  
## 文本  
 如果希望实数被视为 `decimal` 类型，请使用后缀 m 或 M，例如：  
  
```  
  
decimal myMoney = 300.5m;  
```  
  
 如果没有后缀 m，则数字将被视为 [double](../../../csharp/language-reference/keywords/double.md) 类型并会生成编译器错误。  
  
## 转换  
 整型将被隐式转换为 `decimal` 类型，其计算结果为 `decimal`。  因此，你可以使用整数文本初始化十进制变量而不使用后缀，如下所示：  
  
```  
  
decimal myMoney = 300;  
```  
  
 在浮点型和 `decimal` 类型之间不存在隐式转换；因此，必须使用强制转换以在这两个类型之间转换。  例如：  
  
```  
  
        decimal myMoney = 99.9m;  
double x = (double)myMoney;  
myMoney = (decimal)x;  
```  
  
 你还可以在同一表达式中混合使用 `decimal` 和数值整型。  但是，不进行强制转换就混合使用 `decimal` 和浮点型将导致编译错误。  
  
 有关隐式数值转换的更多信息，请参见[隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
 有关显式数值转换的更多信息，请参见[显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)。  
  
## 设置十进制输出的格式  
 你可以通过使用 `String.Format` 方法或 <xref:System.Console.Write%2A?displayProperty=fullName> 方法（其调用 `String.Format()`）来设置结果的格式。  货币格式是使用标准货币格式字符串“C”或“c”指定的，如本文后面的第二个示例所示。  有关 `String.Format` 方法的更多信息，请参见 <xref:System.String.Format%2A?displayProperty=fullName>。  
  
## 示例  
 下面的示例尝试添加 [double](../../../csharp/language-reference/keywords/double.md) 和 `decimal` 变量，这会导致编译器错误。  
  
```c#  
double dub = 9;  
// The following line causes an error that reads "Operator '+' cannot be applied to   
// operands of type 'double' and 'decimal'"  
Console.WriteLine(dec + dub);   
  
// You can fix the error by using explicit casting of either operand.  
Console.WriteLine(dec + (decimal)dub);  
Console.WriteLine((double)dec + dub);  
  
```  
  
 其结果为以下错误：  
  
 `Operator '+' cannot be applied to operands of type 'double' and 'decimal'`  
  
 在此示例中，同一个表达式中混合使用了 `decimal` 和 [int](../../../csharp/language-reference/keywords/int.md)。  计算结果为 `decimal` 类型。  
  
 [!code-cs[csrefKeywordsTypes#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/decimal_1.cs)]  
  
## 示例  
 在此示例中，通过使用货币格式字符串来设置输出的格式。  请注意，`x` 被舍入，因为其小数位数超出了 $0.99。  表示最大精确位数的变量 `y` 严格按照正确的格式显示。  
  
 [!code-cs[csrefKeywordsTypes#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/decimal_2.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Decimal>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)   
 [标准数字格式字符串](../Topic/Standard%20Numeric%20Format%20Strings.md)