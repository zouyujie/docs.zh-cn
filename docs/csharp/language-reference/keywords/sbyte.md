---
title: "sbyte（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sbyte_CSharpKeyword"
  - "sbyte"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "sbyte 关键字 [C#]"
ms.assetid: 1a9c7b48-73d1-4d33-b485-c4faf0a816bc
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# sbyte（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`sbyte` 关键字表示一种整型，该类型根据下表显示的大小和范围存储值。  
  
|类型|范围|大小|.NET Framework 类型|  
|--------|--------|--------|-----------------------|  
|`sbyte`|\-128 到 127|有符号 8 位整数|<xref:System.SByte?displayProperty=fullName>|  
  
## 文本  
 可使用下述方法声明并初始化 `sbyte` 类型的变量：  
  
```  
  
sbyte sByte1 = 127;  
```  
  
 在以上声明中，整数 127 从 [int](../../../csharp/language-reference/keywords/int.md) 隐式转换为 `sbyte`。  如果整数超出了 `sbyte` 的范围，将产生编译错误。  
  
 调用重载方法时必须使用强制转换。  以下面使用 `sbyte` 和 [int](../../../csharp/language-reference/keywords/int.md) 参数的重载方法为例：  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(sbyte b) {}  
```  
  
 使用 `sbyte` 强制转换可保证调用正确的类型，例如：  
  
```  
// Calling the method with the int parameter:  
SampleMethod(5);  
// Calling the method with the sbyte parameter:  
SampleMethod((sbyte)5);  
```  
  
## 转换  
 存在从 `sbyte` 到 [short](../../../csharp/language-reference/keywords/short.md)、[int](../../../csharp/language-reference/keywords/int.md)、[long](../../../csharp/language-reference/keywords/long.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 的预定义隐式转换。  
  
 不能将存储大小更大的非文本数值类型隐式转换为 `sbyte` 类型（有关整型的存储大小的信息，请参见 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)）。  例如，请看以下两个 `sbyte` 变量 `x` 和 `y`：  
  
```  
  
sbyte x = 10, y = 20;  
```  
  
 以下赋值语句将产生一个编译错误，原因是赋值运算符右侧的算术表达式在默认情况下的计算结果为 [int](../../../csharp/language-reference/keywords/int.md)。  
  
```  
  
sbyte z = x + y;   // Error: conversion from int to sbyte  
```  
  
 若要更正此问题，请对该表达式执行强制转换，如下例所示：  
  
```  
  
sbyte z = (sbyte)(x + y);   // OK: explicit conversion  
```  
  
 但是，在目标变量具有相同或更大的存储大小时，使用下列语句是可能的：  
  
```  
  
        sbyte x = 10, y = 20;  
int m = x + y;  
long n = x + y;  
```  
  
 还请注意，不存在从浮点型到 `sbyte` 类型的隐式转换。  例如，除非使用显式强制转换，否则以下语句将生成一个编译器错误：  
  
```  
  
        sbyte x = 3.0;         // Error: no implicit conversion from double  
sbyte y = (sbyte)3.0;  // OK: explicit conversion  
```  
  
 有关兼用浮点型和整型的算术表达式的信息，请参见 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 有关隐式数值转换规则的更多信息，请参见[隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 <xref:System.SByte>   
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)