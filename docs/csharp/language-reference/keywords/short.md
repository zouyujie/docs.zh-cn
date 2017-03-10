---
title: "short（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "short"
  - "short_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "short 关键字 [C#]"
ms.assetid: 04c10688-e51a-4a87-bfec-83f7fb42ff11
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# short（C# 参考）
`short` 关键字表示一种整数数据类型，该类型根据下表显示的大小和范围存储值。  
  
|类型|范围|大小|.NET Framework 类型|  
|--------|--------|--------|-----------------------|  
|`short`|\-32,768 到 32,767|有符号 16 位整数|<xref:System.Int16?displayProperty=fullName>|  
  
## 文本  
 可如下例所示声明并初始化 `short` 类型的变量：  
  
```  
  
short x = 32767;  
```  
  
 在以上声明中，整数 `32767` 从 [int](../../../csharp/language-reference/keywords/int.md) 隐式转换为 `short`。  如果整数的长度超过了 `short` 存储位置的大小，则将产生编译错误。  
  
 调用重载方法时必须使用强制转换。  以下面使用 `short` 和 [int](../../../csharp/language-reference/keywords/int.md) 参数的重载方法为例：  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(short s) {}  
```  
  
 使用 `short` 强制转换可保证调用正确的类型，例如：  
  
```  
SampleMethod(5);         // Calling the method with the int parameter  
SampleMethod((short)5);  // Calling the method with the short parameter  
```  
  
## 转换  
 存在从 `short` 到 [int](../../../csharp/language-reference/keywords/int.md)、[long](../../../csharp/language-reference/keywords/long.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 的预定义隐式转换。  
  
 不能将存储大小更大的非文本数值类型隐式转换为 `short` 类型（有关整型的存储大小的信息，请参见 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)）。  例如，请看以下两个 `short` 变量 `x` 和 `y`：  
  
```  
  
short x = 5, y = 12;  
```  
  
 以下赋值语句将产生一个编译错误，原因是赋值运算符右侧的算术表达式在默认情况下的计算结果为 [int](../../../csharp/language-reference/keywords/int.md) 类型。  
  
 `short`   `z = x + y;   // Error: no conversion from int to short`  
  
 若要解决此问题，请使用强制转换：  
  
 `short`   `z = (`  `short`  `)(x + y);   // OK: explicit conversion`  
  
 但是，在目标变量具有相同或更大的存储大小时，使用下列语句是可能的：  
  
```  
int m = x + y;  
long n = x + y;  
```  
  
 不存在从浮点型到 `short` 类型的隐式转换。  例如，除非使用显式强制转换，否则以下语句将生成一个编译器错误：  
  
```  
  
        short x = 3.0;          // Error: no implicit conversion from double  
short y = (short)3.0;   // OK: explicit conversion  
```  
  
 有关兼用浮点型和整型的算术表达式的信息，请参见 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 有关隐式数值转换规则的更多信息，请参见 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Int16>   
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)