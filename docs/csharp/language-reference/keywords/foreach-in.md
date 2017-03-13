---
title: "foreach，in（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "foreach"
  - "foreach_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "foreach 关键字 [C#]"
  - "foreach 语句 [C#]"
  - "in 关键字 [C#]"
ms.assetid: 5a9c5ddc-5fd3-457a-9bb6-9abffcd874ec
caps.latest.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 29
---
# foreach，in（C# 参考）
`foreach` 语句对实现 <xref:System.Collections.IEnumerable?displayProperty=fullName> 或 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> 接口的数组或对象集合中的每个元素重复一组嵌入式语句。  `foreach` 语句用于循环访问集合，以获取您需要的信息，但不能用于在源集合中添加或移除项，否则可能产生不可预知的副作用。  如果需要在源集合中添加或移除项，请使用 [for](../../../csharp/language-reference/keywords/for.md) 循环。  
  
 嵌入语句为数组或集合中的每个元素继续执行。  当为集合中的所有元素完成迭代后，控制传递给 `foreach` 块之后的下一个语句。  
  
 可以在 `foreach` 块的任何点使用 [break](../../../csharp/language-reference/keywords/break.md) 关键字跳出循环，或使用 [continue](../../../csharp/language-reference/keywords/continue.md) 关键字进入循环的下一轮迭代。  
  
 `foreach` 循环还可以通过 [goto](../../../csharp/language-reference/keywords/goto.md)、[return](../../../csharp/language-reference/keywords/return.md) 或 [throw](../../../csharp/language-reference/keywords/throw.md) 语句退出。  
  
 有关 `foreach` 关键字和代码示例的更多信息，请参见下面的主题：  
  
 [对数组使用 foreach](../../../csharp/programming-guide/arrays/using-foreach-with-arrays.md)  
  
 [如何：使用 foreach 访问集合类](../../../csharp/programming-guide/classes-and-structs/how-to-access-a-collection-class-with-foreach.md)  
  
## 示例  
 以下代码显示了三个示例：  
  
-   显示整数数组内容的典型的 `foreach` 循环  
  
-   执行相同操作的 [for](../../../csharp/language-reference/keywords/for.md) 循环  
  
-   维护数组中的元素数计数的 `foreach` 循环  
  
 [!code-cs[csrefKeywordsIteration#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/foreach-in_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [迭代语句](../../../csharp/language-reference/keywords/iteration-statements.md)   
 [for](../../../csharp/language-reference/keywords/for.md)