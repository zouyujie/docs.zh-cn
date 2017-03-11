---
title: "byte（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "byte"
  - "byte_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "byte 关键字 [C#]"
ms.assetid: 111f1db9-ca32-4f0e-b497-4783517eda47
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# byte（C# 参考）
`byte` 关键字代表一种整型，该类型按下表所示存储值：  
  
|类型|范围|大小|.NET Framework 类型|  
|--------|--------|--------|-----------------------|  
|`byte`|0 到 255|无符号 8 位整数|<xref:System.Byte?displayProperty=fullName>|  
  
## 文本  
 可如下例所示声明并初始化 `byte` 类型的变量：  
  
```  
byte myByte = 255;  
```  
  
 在以上声明中，整数 `255` 从 [int](../../../csharp/language-reference/keywords/int.md) 隐式转换为 `byte`。  如果整数超出了 `byte` 的范围，将产生编译错误。  
  
## 转换  
 存在从 `byte` 到 [short](../../../csharp/language-reference/keywords/short.md)、[ushort](../../../csharp/language-reference/keywords/ushort.md)、[int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 的预定义隐式转换。  
  
 不能将更大存储大小的非文本数值类型隐式转换为 `byte`。  有关整型的存储大小的更多信息，请参见 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)。  例如，请看以下两个 `byte` 变量 `x` 和 `y`：  
  
```  
  
byte x = 10, y = 20;  
```  
  
 以下赋值语句将产生一个编译错误，原因是赋值运算符右侧的算术表达式在默认情况下的计算结果为 `int` 类型。  
  
```  
// Error: conversion from int to byte:  
byte z = x + y;  
```  
  
 若要解决此问题，请使用强制转换：  
  
```  
// OK: explicit conversion:  
byte z = (byte)(x + y);  
```  
  
 但是，在目标变量具有相同或更大的存储大小时，使用下列语句是可能的：  
  
```  
int x = 10, y = 20;  
int m = x + y;  
long n = x + y;  
```  
  
 同样，不存在从浮点型到 `byte` 类型的隐式转换。  例如，除非使用显式强制转换，否则以下语句将生成一个编译器错误：  
  
```  
// Error: no implicit conversion from double:  
byte x = 3.0;   
// OK: explicit conversion:  
byte y = (byte)3.0;  
```  
  
 调用重载方法时，必须使用显式转换。  以下面使用 `byte` 和 [int](../../../csharp/language-reference/keywords/int.md) 参数的重载方法为例：  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(byte b) {}  
```  
  
 使用 `byte` 强制转换可保证调用正确的类型，例如：  
  
```  
// Calling the method with the int parameter:  
SampleMethod(5);  
// Calling the method with the byte parameter:  
SampleMethod((byte)5);  
```  
  
 有关兼用浮点型和整型的算术表达式的信息，请参见 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 有关隐式数值转换规则的更多信息，请参见 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Byte>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)