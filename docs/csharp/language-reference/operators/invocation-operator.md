---
title: "() 运算符（C# 参考） | Microsoft Docs"
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
  - "()_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "() 运算符 [C#]"
  - "强制转换运算符 [C#]"
  - "类型转换 [C#], () 运算符"
ms.assetid: 846e1f94-8a8c-42fc-a42c-fbd38e70d8cc
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# () 运算符（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

除了用于指定表达式中运算符的顺序外，圆括号还用于执行以下任务：  
  
1.  指定强制转换或类型转换。  
  
     [!code-cs[csRefOperators#1](../../../csharp/language-reference/operators/codesnippet/CSharp/invocation-operator_1.cs)]  
  
2.  调用方法或委托。  
  
     [!code-cs[csRefOperators#2](../../../csharp/language-reference/operators/codesnippet/CSharp/invocation-operator_2.cs)]  
  
## 备注  
 强制转换显式调用从一种类型到另一种类型的转换运算符；如果未定义这样的转换运算符，则强制转换将失败。  若要定义转换运算符，请参见 [explicit](../../../csharp/language-reference/keywords/explicit.md) 和 [implicit](../../../csharp/language-reference/keywords/implicit.md)。  
  
 不能重载 `()` 运算符。  
  
 有关更多信息，请参见 [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)。  
  
 强制转换表达式可能会使语法发生歧义。  例如，表达式 `(x)–y` 既可以解释为强制转换表达式（将 –y 强制转换为类型 x），也可以解释为结合了带括号表达式的相加表达式（计算 x – y 的值）。  
  
 有关方法调用的详细信息，请参阅[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)