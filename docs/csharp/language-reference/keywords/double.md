---
title: "double（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "double"
  - "double_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "双精度数据类型 [C#]"
ms.assetid: 0980e11b-6004-4102-abcf-cfc280fc6991
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# double（C# 参考）
`double` 关键字表示存储 64 位浮点值的简单类型。  下表显示了 `double` 类型的精度和大致范围。  
  
|类型|大致范围|精度|.NET Framework 类型|  
|--------|----------|--------|-----------------------|  
|`double`|±5.0 × 10<sup>−324</sup> 到 ±1.7 × 10<sup>308</sup>|15 到 16 位|<xref:System.Double?displayProperty=fullName>|  
  
## 文本  
 默认情况下，赋值运算符右侧的实数被视为 `double`。  但是，如果希望整数被视为 `double`，请使用后缀 d 或 D，例如：  
  
```  
  
double x = 3D;  
```  
  
## 转换  
 可在一个表达式中兼用数值整型和浮点型。  在此情况下，整型将转换为浮点型。  根据以下规则计算表达式：  
  
-   如果其中一个浮点类型为 `double`，则表达式的计算结果为 `double` 或 [bool](../../../csharp/language-reference/keywords/bool.md)（在关系表达式或布尔表达式中）。  
  
-   如果表达式中不存在 `double` 类型，则表达式的计算结果为 [float](../../../csharp/language-reference/keywords/float.md) 或 [bool](../../../csharp/language-reference/keywords/bool.md)（在关系表达式或布尔表达式中）。  
  
 浮点表达式可以包含下列值集：  
  
-   正零和负零。  
  
-   正无穷和负无穷。  
  
-   非数字值 \(NaN\)。  
  
-   有限的非零值集。  
  
 有关这些值的更多信息，请参见 [IEEE](http://go.microsoft.com/fwlink/?LinkId=26269) 网站上的“IEEE Standard for Binary Floating\-Point Arithmetic”（二进制浮点算法的 IEEE 标准）。  
  
## 示例  
 在下面的示例中，一个 [int](../../../csharp/language-reference/keywords/int.md)、一个 [short](../../../csharp/language-reference/keywords/short.md)、一个 [float](../../../csharp/language-reference/keywords/float.md) 和一个 `double` 相加，计算结果为 `double` 类型。  
  
 [!code-cs[csrefKeywordsTypes#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/double_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [默认值表](../../../csharp/language-reference/keywords/default-values-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [浮点型表](../../../csharp/language-reference/keywords/floating-point-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)