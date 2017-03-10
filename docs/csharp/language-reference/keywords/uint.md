---
title: "uint（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "uint"
  - "uint_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "uint 关键字 [C#]"
ms.assetid: e93e42c6-ec72-4b0b-89df-2fd8d36f7a7b
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# uint（C# 参考）
`uint` 关键字表示一种整型，该类型根据下表显示的大小和范围存储值。  
  
|类型|范围|大小|.NET Framework 类型|  
|--------|--------|--------|-----------------------|  
|`uint`|0 到 4,294,967,295|无符号 32 位整数|<xref:System.UInt32?displayProperty=fullName>|  
  
 **注意** `uint` 类型与 CLS 不兼容。  应尽可能使用 `int`。  
  
## 文本  
 可如下例所示声明并初始化 `uint` 类型的变量：  
  
```  
  
uint myUint = 4294967290;  
```  
  
 如果整数没有后缀，则其类型为以下类型中可表示其值的第一个类型：[int](../../../csharp/language-reference/keywords/int.md)、`uint`、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)。  在此例中，它是 `uint`：  
  
```  
  
uint uInt1 = 123;  
```  
  
 还可以像下面这样使用后缀 u 或 U：  
  
```  
  
uint uInt2 = 123U;  
```  
  
 当使用后缀 `U` 或 `u` 时，将根据文本的数值来确定文本的类型是 `uint` 还是 `ulong`。  例如：  
  
```  
Console.WriteLine(44U.GetType());  
Console.WriteLine(323442434344U.GetType());  
```  
  
 此代码先后显示 `System.UInt32` 和 `System.UInt64`（它们分别是 `uint` 和 `ulong` 的基础类型），因为第二个文本太大，无法用 `uint` 类型来存储。  
  
## 转换  
 存在从 `uint` 到 [long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 的预定义隐式转换。  例如：  
  
```  
float myFloat = 4294967290;   // OK: implicit conversion to float  
```  
  
 存在从 [byte](../../../csharp/language-reference/keywords/byte.md)、[ushort](../../../csharp/language-reference/keywords/ushort.md) 或 [char](../../../csharp/language-reference/keywords/char.md) 到 `uint` 的预定义隐式转换。  否则必须使用显式转换。  例如，如果不进行强制转换，下面的赋值语句将产生编译错误：  
  
```  
long aLong = 22;  
// Error -- no implicit conversion from long:  
uint uInt1 = aLong;   
// OK -- explicit conversion:  
uint uInt2 = (uint)aLong;  
```  
  
 还请注意，不存在从浮点型到 `uint` 类型的隐式转换。  例如，除非使用显式强制转换，否则以下语句将生成一个编译器错误：  
  
```  
// Error -- no implicit conversion from double:  
uint x = 3.0;  
// OK -- explicit conversion:  
uint y = (uint)3.0;   
```  
  
 有关兼用浮点型和整型的算术表达式的信息，请参见 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 有关隐式数值转换规则的更多信息，请参见[隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.UInt32>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)