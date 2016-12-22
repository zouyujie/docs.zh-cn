---
title: "ulong（C# 参考） | Microsoft Docs"
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
  - "ulong_CSharpKeyword"
  - "ulong"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "ulong 关键字 [C#]"
ms.assetid: f2ece624-837a-40cf-92c5-343e7f33397c
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# ulong（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`ulong` 关键字表示一种整型，该类型根据下表显示的大小和范围存储值。  
  
|类型|范围|大小|.NET Framework 类型|  
|--------|--------|--------|-----------------------|  
|`ulong`|0 到 18,446,744,073,709,551,615|无符号 64 位整数|<xref:System.UInt64?displayProperty=fullName>|  
  
## 文本  
 可如下例所示声明并初始化 `ulong` 类型的变量：  
  
```  
  
ulong uLong = 9223372036854775808;  
```  
  
 如果整数没有后缀，则其类型为以下类型中可表示其值的第一个类型：[int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、`ulong`。  在上面的示例中，它是 `ulong` 类型。  
  
 还可根据以下规则使用后缀指定文字类型：  
  
-   如果使用 L 或 l，那么根据整数的大小，可以判断出其类型为 [long](../../../csharp/language-reference/keywords/long.md) 还是 `ulong`。  
  
    > [!NOTE]
    >  注意也可用小写字母“l”作后缀。  但是，因为字母“l”容易与数字“1”混淆，会生成编译器警告。为清楚起见，请使用“L”。  
  
-   如果使用 `U` 或 `u`，那么根据整数的大小，可以判断出其类型为 [uint](../../../csharp/language-reference/keywords/uint.md) 还是 `ulong`。  
  
-   如果使用 UL、ul、Ul、uL、LU、lu、Lu 或 lU，则整数的类型为 `ulong`。  
  
     例如，以下三个语句的输出将为系统类型 `UInt64`，此类型对应于别名 `ulong`：  
  
    ```  
    Console.WriteLine(9223372036854775808L.GetType());  
    Console.WriteLine(123UL.GetType());  
    Console.WriteLine((123UL + 456).GetType());  
    ```  
  
 此后缀常用于调用重载方法。  以下面使用 `ulong` 和 [int](../../../csharp/language-reference/keywords/int.md) 参数的重载方法为例：  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(ulong l) {}  
```  
  
 在 `ulong` 参数后加上后缀可保证调用正确的类型，例如：  
  
```  
SampleMethod(5);    // Calling the method with the int parameter  
SampleMethod(5UL);  // Calling the method with the ulong parameter  
```  
  
## 转换  
 存在从 `ulong` 到 [float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 的预定义隐式转换。  
  
 不存在从 `ulong` 到任何整型的隐式转换。  例如，不使用显式类型转换时，下列语句将产生编译错误：  
  
```  
long long1 = 8UL;   // Error: no implicit conversion from ulong  
```  
  
 存在从 [byte](../../../csharp/language-reference/keywords/byte.md)、[ushort](../../../csharp/language-reference/keywords/ushort.md)、[uint](../../../csharp/language-reference/keywords/uint.md) 或 [char](../../../csharp/language-reference/keywords/char.md) 到 `ulong` 的预定义隐式转换。  
  
 同样，不存在从浮点型到 `ulong` 类型的隐式转换。  例如，除非使用显式强制转换，否则以下语句将生成一个编译器错误：  
  
```  
// Error -- no implicit conversion from double:  
ulong x = 3.0;  
// OK -- explicit conversion:  
ulong y = (ulong)3.0;    
```  
  
 有关兼用浮点型和整型的算术表达式的信息，请参见 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 有关隐式数值转换规则的更多信息，请参见 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 <xref:System.UInt64>   
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)