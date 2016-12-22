---
title: "let 子句（C# 参考） | Microsoft Docs"
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
  - "let_CSharpKeyword"
  - "let"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "let 子句 [C#]"
  - "let 关键字 [C#]"
ms.assetid: 13c9c1a4-ce57-48ef-8e1b-4c2a59b99fb4
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# let 子句（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在查询表达式中，存储子表达式的结果有时很有用，这样可以在随后的子句中使用。  可以使用 `let` 关键字完成这一工作，该关键字可以创建一个新的范围变量，并且用您提供的表达式的结果初始化该变量。  一旦用值初始化了该范围变量，它就不能用于存储其他值。  但如果该范围变量存储的是可查询的类型，则可以对其进行查询。  
  
## 示例  
 在下面的示例中，以两种方式使用了 `let`：  
  
1.  创建一个可以查询自身的可枚举类型。  
  
2.  使查询只能对范围变量 `word` 调用一次 `ToLower`。  如果不使用 `let`，则必须在 `where` 子句的每个谓词中调用 `ToLower`。  
  
 [!code-cs[cscsrefQueryKeywords#28](../../../csharp/language-reference/keywords/codesnippet/CSharp/let-clause_1.cs)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 查询表达式](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [如何：在查询表达式中处理异常](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md)