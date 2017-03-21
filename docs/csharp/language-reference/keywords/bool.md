---
title: "bool（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "bool_CSharpKeyword"
  - "bool"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "bool 关键字 [C#]"
ms.assetid: 551cfe35-2632-4343-af49-33ad12da08e2
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# bool（C# 参考）
`bool` 关键字是 <xref:System.Boolean?displayProperty=fullName> 的别名。  它用于声明变量来存储布尔值 [true](../../../csharp/language-reference/keywords/true.md) 和 [false](../../../csharp/language-reference/keywords/false.md)。  
  
> [!NOTE]
>  如果需要一个也可以有 `null` 值的布尔型变量，请使用 `bool?`。  有关更多信息，请参见 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)。  
  
## 文本  
 可将布尔值赋给 `bool` 变量。  也可以将计算结果为 `bool` 类型的表达式赋给 `bool` 变量。  
  
 [!code-cs[csrefKeywordsTypes#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/bool_1.cs)]  
  
 `bool` 变量的默认值为 `false`。  `bool?` 变量的默认值为 `null`。  
  
## 转换  
 在 C\+\+ 中，`bool` 类型的值可转换为 `int` 类型的值；也就是说，`false` 等效于零值，而 `true` 等效于非零值。  在 C\# 中，不存在 `bool` 类型与其他类型之间的相互转换。  例如，下面的 `if` 语句在 C\# 中无效：  
  
 [!code-cs[csrefKeywordsTypes#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/bool_2.cs)]  
  
 若要测试 `int` 类型的变量，必须将该变量与一个值（例如零）进行显式比较，如下所示：  
  
 [!code-cs[csrefKeywordsTypes#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/bool_3.cs)]  
  
## 示例  
 在此例中，您从键盘输入一个字符，然后程序检查输入的字符是否是一个字母。  如果字符是一个字母，则程序检查它是大写还是小写。  这些检查是使用 <xref:System.Char.IsLetter%2A> 和 <xref:System.Char.IsLower%2A>（两者均返回 `bool` 类型）来执行的：  
  
 [!code-cs[csrefKeywordsTypes#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/bool_4.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)