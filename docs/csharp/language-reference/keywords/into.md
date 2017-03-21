---
title: "into（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "into_CSharpKeyword"
  - "into"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "into 关键字 [C#]"
ms.assetid: 81ec62c1-f0b1-4755-8a31-959876e77f65
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# into（C# 参考）
可以使用 `into` 上下文关键字创建一个临时标识符，以便将 [group](../../../csharp/language-reference/keywords/group-clause.md)、[join](../../../csharp/language-reference/keywords/join-clause.md) 或 [select](../../../csharp/language-reference/keywords/select-clause.md) 子句的结果存储到新的标识符中。  此标识符本身可以是附加查询命令的生成器。  在 `group` 或 `select` 子句中使用新标识符的用法有时称为“延续”。  
  
## 示例  
 下面的示例演示使用 `into` 关键字来启用临时标识符 `fruitGroup`，该标识符具有推断类型 `IGrouping`。  通过使用该标识符，可以对每个组调用 <xref:System.Linq.Enumerable.Count%2A> 方法，并且仅选择那些包含两个或更多个单词的组。  
  
 [!code-cs[cscsrefQueryKeywords#18](../../../csharp/language-reference/keywords/codesnippet/CSharp/into_1.cs)]  
  
 仅当希望对每个组执行附加查询操作时，才需要在 `group` 子句中使用 `into`。  有关更多信息，请参见 [group 子句](../../../csharp/language-reference/keywords/group-clause.md)。  
  
 有关在 `join` 子句中使用 `into` 的示例，请参见 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)。  
  
## 请参阅  
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [group 子句](../../../csharp/language-reference/keywords/group-clause.md)