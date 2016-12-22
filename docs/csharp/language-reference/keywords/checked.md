---
title: "checked（C# 参考） | Microsoft Docs"
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
  - "checked_CSharpKeyword"
  - "checked"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "checked 关键字 [C#]"
ms.assetid: 718a1194-988d-48a3-b089-d6ee8bd1608d
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# checked（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`checked` 关键字用于对整型算术运算和转换显式启用溢出检查。  
  
 默认情况下，如果表达式仅包含常数值，且产生的值在目标类型范围之外，则它会导致编译器错误。  如果表达式包含一个或多个非常数值，则编译器不检测溢出。  在下面的示例中，计算赋给 `i2` 的表达式不会导致编译器错误。  
  
 [!CODE [csrefKeywordsChecked#3](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsChecked#3)]  
  
 默认情况下，在运行时也不检查这些非常数表达式是否溢出，这些表达式不引发溢出异常。  上面的示例显示 \-2,147,483,639 作为两个正整数之和。  
  
 可以通过编译器选项、环境配置或使用 `checked` 关键字来启用溢出检查。  下面的示例演示如何使用 `checked` 表达式或 `checked` 块，在运行时检测由前面的求和计算导致的溢出。  两个示例都引发溢出异常。  
  
 [!CODE [csrefKeywordsChecked#4](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsChecked#4)]  
  
 可以使用 [unchecked](../../../csharp/language-reference/keywords/unchecked.md) 关键字阻止溢出检查。  
  
## 示例  
 此示例演示如何使用 `checked` 启用运行时溢出检查。  
  
 [!CODE [csrefKeywordsChecked#1](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsChecked#1)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [Checked 和 Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)   
 [unchecked](../../../csharp/language-reference/keywords/unchecked.md)