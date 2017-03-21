---
title: "orderby 子句（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "orderby"
  - "orderby_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "orderby 子句 [C#]"
  - "orderby 关键字 [C#]"
ms.assetid: 21f87f48-d69d-4e95-9a52-6fec47b37e1f
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# orderby 子句（C# 参考）
在查询表达式中，`orderby` 子句可使返回的序列或子序列（组）按升序或降序排序。  可以指定多个键，以便执行一个或多个次要排序操作。  排序是由针对元素类型的默认比较器执行的。  默认排序顺序为升序。  您还可以指定自定义比较器。  但是，只能通过基于方法的语法使用它。  有关更多信息，请参见 [Sorting Data](../../../visual-basic/programming-guide/concepts/linq/sorting-data.md)。  
  
## 示例  
 在下面的示例中，第一个查询按从 A 开始的字母顺序对单词进行排序，第二个查询按降序对相同的单词进行排序。  （`ascending` 关键字是默认排序值，可以省略。）  
  
 [!code-cs[cscsrefQueryKeywords#20](../../../csharp/language-reference/keywords/codesnippet/CSharp/orderby-clause_1.cs)]  
  
## 示例  
 下面的示例对学生的姓氏执行主要排序，然后对他们的名字执行次要排序。  
  
 [!code-cs[cscsrefQueryKeywords#22](../../../csharp/language-reference/keywords/codesnippet/CSharp/orderby-clause_2.cs)]  
  
## 备注  
 编译时，`orderby` 子句被转换为对 <xref:System.Linq.Enumerable.OrderBy%2A> 方法的调用。  `orderby` 子句中的多个键转换为 <xref:System.Linq.Enumerable.ThenBy%2A> 方法调用。  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [group 子句](../../../csharp/language-reference/keywords/group-clause.md)   
 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)