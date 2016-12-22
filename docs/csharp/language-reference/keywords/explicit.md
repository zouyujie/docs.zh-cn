---
title: "explicit（C# 参考） | Microsoft Docs"
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
  - "explicit_CSharpKeyword"
  - "explicit"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "explicit 关键字 [C#]"
ms.assetid: cfb8f42a-e411-4db2-af9b-796b05644846
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# explicit（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`explicit` 关键字用于声明必须使用强制转换来调用的用户定义的类型转换运算符。  例如，在下面的示例中，此运算符将名为 Fahrenheit 的类转换为名为 Celsius 的类：  
  
 [!code-cs[csrefKeywordsConversion#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/explicit_1.cs)]  
  
 可以如下所示调用此转换运算符：  
  
 [!code-cs[csrefKeywordsConversion#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/explicit_2.cs)]  
  
 转换运算符将源类型转换为目标类型。  源类型提供转换运算符。  与隐式转换不同，必须通过强制转换的方式来调用显式转换运算符。  如果转换操作可能导致异常或丢失信息，则应将其标记为 `explicit`。  这可以防止编译器无提示地调用可能产生无法预见后果的转换操作。  
  
 省略此强制转换将导致编译时错误 CS0266。  
  
 有关更多信息，请参见[使用转换运算符](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md)。  
  
## 示例  
 下面的示例提供 `Fahrenheit` 和 `Celsius` 类，它们中的每一个都为另一个提供显式转换运算符。  
  
 [!code-cs[csrefKeywordsConversion#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/explicit_3.cs)]  
  
## 示例  
 下面的示例定义一个结构 `Digit`，该结构表示单个十进制数字。  定义了一个运算符，用于将 `byte` 转换为 `Digit`，但因为并非所有字节都可以转换为 `Digit`，所以该转换是显式的。  
  
 [!code-cs[csrefKeywordsConversion#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/explicit_4.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [implicit](../../../csharp/language-reference/keywords/implicit.md)   
 [运算符](../../../csharp/language-reference/keywords/operator.md)   
 [如何：在结构之间实现用户定义的转换](../Topic/How%20to:%20Implement%20User-Defined%20Conversions%20Between%20Structs%20\(C%23%20Programming%20Guide\).md)   
 [链接的用户定义的显式转换在 C\#](http://go.microsoft.com/fwlink/?LinkId=112384)