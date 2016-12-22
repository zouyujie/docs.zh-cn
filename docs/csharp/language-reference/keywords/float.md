---
title: "float（C# 参考） | Microsoft Docs"
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
  - "float"
  - "float_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "float 关键字 [C#]"
  - "浮点数 [C#], float 关键字"
ms.assetid: 1e77db7b-dedb-48b7-8dd1-b055e96a9258
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# float（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`float` 关键字表示存储 32 位浮点值的简单类型。  下表显示了 `float` 类型的精度和大致范围。  
  
|类型|大致范围|精度|.NET Framework 类型|  
|--------|----------|--------|-----------------------|  
|`float`|\-3.4 × 10<sup>38</sup> 到 \+3.4 × 10<sup>38</sup>|7 位|<xref:System.Single?displayProperty=fullName>|  
  
## 文本  
 默认情况下，赋值运算符右侧的实数被视为 [double](../../../csharp/language-reference/keywords/double.md)。  因此，应使用后缀 `f` 或 `F` 初始化浮点型变量，如以下示例中所示：  
  
```  
  
float x = 3.5F;  
```  
  
 如果在以上声明中不使用后缀，则会因为您尝试将一个 [double](../../../csharp/language-reference/keywords/double.md) 值存储到 `float` 变量中而发生编译错误。  
  
## 转换  
 可在一个表达式中兼用数值整型和浮点型。  在此情况下，整型将转换为浮点型。  根据以下规则计算表达式：  
  
-   如果其中一个浮点型为 [double](../../../csharp/language-reference/keywords/double.md)，则表达式的计算结果为 [double](../../../csharp/language-reference/keywords/double.md) 或 [bool](../../../csharp/language-reference/keywords/bool.md)（在关系表达式或布尔表达式中）。  
  
-   如果表达式中不存在 [double](../../../csharp/language-reference/keywords/double.md) 类型，则表达式的计算结果为 `float` 或 [bool](../../../csharp/language-reference/keywords/bool.md)（在关系表达式或布尔表达式中）。  
  
 浮点表达式可以包含下列值集：  
  
-   正零和负零  
  
-   正无穷和负无穷  
  
-   非数字值 \(NaN\)  
  
-   有限的非零值集  
  
 有关这些值的更多信息，请参见 [IEEE](http://go.microsoft.com/fwlink/?LinkId=26269) 网站上的“IEEE Standard for Binary Floating\-Point Arithmetic”（二进制浮点算法的 IEEE 标准）。  
  
## 示例  
 在下面的示例中，包含 [int](../../../csharp/language-reference/keywords/int.md)、[short](../../../csharp/language-reference/keywords/short.md) 和 `float` 类型的数学表达式得到一个 `float` 结果。  （请记住 `float` 是 <xref:System.Single?displayProperty=fullName> 类型的别名。）请注意，表达式中没有 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 [!code-cs[csrefKeywordsTypes#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/float_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 <xref:System.Single>   
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)