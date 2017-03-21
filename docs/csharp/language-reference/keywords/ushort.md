---
title: "ushort（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "ushort"
  - "ushort_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "ushort 关键字 [C#]"
ms.assetid: 1a7dbaae-b7a0-4111-872a-c88a6d3981ac
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# ushort（C# 参考）
`ushort` 关键字表示整数数据类型，该类型根据下表显示的大小和范围存储值。  
  
|类型|范围|大小|.NET Framework 类型|  
|--------|--------|--------|-----------------------|  
|`ushort`|0 到 65,535|无符号 16 位整数|<xref:System.UInt16?displayProperty=fullName>|  
  
## 文本  
 可如下例所示声明并初始化 `ushort` 类型的变量：  
  
```  
  
ushort myShort = 65535;  
```  
  
 在以上声明中，整数 `65535` 从 [int](../../../csharp/language-reference/keywords/int.md) 隐式转换为 `ushort`。  如果整数超出了 `ushort` 的范围，将产生编译错误。  
  
 调用重载方法时，必须使用强制转换。  以下面使用 `ushort` 和 [int](../../../csharp/language-reference/keywords/int.md) 参数的重载方法为例：  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(ushort s) {}  
```  
  
 使用 `ushort` 强制转换可保证调用正确的类型，例如：  
  
```  
// Calls the method with the int parameter:  
SampleMethod(5);  
// Calls the method with the ushort parameter:  
SampleMethod((ushort)5);    
```  
  
## 转换  
 存在从 `ushort` 到 [int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 的预定义隐式转换。  
  
 存在从 [byte](../../../csharp/language-reference/keywords/byte.md) 或 [char](../../../csharp/language-reference/keywords/char.md) 到 `ushort` 的预定义隐式转换。  其他情况下必须使用显式转换。  例如，请看以下两个 `ushort` 变量 `x` 和 `y`：  
  
```  
  
ushort x = 5, y = 12;  
```  
  
 以下赋值语句将产生一个编译错误，原因是赋值运算符右侧的算术表达式在默认情况下的计算结果为 `int`。  
  
```  
  
ushort z = x + y;   // Error: conversion from int to ushort  
```  
  
 若要解决此问题，请使用强制转换：  
  
```  
  
ushort z = (ushort)(x + y);   // OK: explicit conversion   
```  
  
 但是，在目标变量具有相同或更大的存储大小时，使用下列语句是可能的：  
  
```  
int m = x + y;  
long n = x + y;  
```  
  
 还请注意，不存在从浮点型到 `ushort` 类型的隐式转换。  例如，除非使用显式强制转换，否则以下语句将生成一个编译器错误：  
  
```  
// Error -- no implicit conversion from double:  
ushort x = 3.0;   
// OK -- explicit conversion:  
ushort y = (ushort)3.0;  
```  
  
 有关兼用浮点型和整型的算术表达式的信息，请参见 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 有关隐式数值转换规则的更多信息，请参见[隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.UInt16>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)