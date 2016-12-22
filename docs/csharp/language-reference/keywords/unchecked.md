---
title: "unchecked（C# 参考） | Microsoft Docs"
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
  - "unchecked_CSharpKeyword"
  - "unchecked"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "unchecked 关键字 [C#]"
ms.assetid: 0c021f7c-923f-4b3d-a58f-55336f5ac27e
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# unchecked（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`unchecked` 关键字用于取消整型算术运算和转换的溢出检查。  
  
 在未检查的上下文中，如果表达式产生的值在目标类型范围之外，并不会标记溢出。  例如，下例中的计算在 `unchecked` 块或表达式中执行，因此将忽略结果对于整数而言过大这一事实，并会对 `int1` 赋予值 \-2,147,483,639。  
  
 [!CODE [csrefKeywordsChecked#5](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsChecked#5)]  
  
 如果移除 `unchecked` 环境，则发生编译错误。  因为表达式的各个项都是常数，所以可以在编译时检测到溢出。  
  
 默认情况下，在编译时和运行时不检查包含非常数项的表达式。  有关启用检查环境的信息，请参见 [checked](../../../csharp/language-reference/keywords/checked.md)。  
  
 因为溢出检查比较耗时，所以当无溢出危险时，使用不检查的代码可以提高性能。  但是，如果可能发生溢出，则应使用检查环境。  
  
## 示例  
 此示例演示如何使用 `unchecked` 关键字。  
  
 [!CODE [csrefKeywordsChecked#2](../CodeSnippet/VS_Snippets_VBCSharp/csrefKeywordsChecked#2)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [Checked 和 Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)   
 [checked](../../../csharp/language-reference/keywords/checked.md)