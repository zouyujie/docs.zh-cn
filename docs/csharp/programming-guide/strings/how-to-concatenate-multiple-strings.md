---
title: "如何：串联多个字符串（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "串联字符串 [C#]"
  - "联接字符串 [C#]"
  - "字符串 [C#], 串联"
ms.assetid: 8e16736f-4096-4f3f-be0f-9d4c3ff63520
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# 如何：串联多个字符串（C# 编程指南）
串联是将一个字符串追加到另一个字符串末尾的过程。  使用 `+` 运算符串联字符串文本或字符串常量时，编译器会创建一个字符串。  串联不在运行时发生。  但字符串变量只能在运行时串联，  对此，您应该了解各种方法的性能含义。  
  
## 示例  
 下面的示例演示如何将一个长字符串拆分为几个较短的字符串，从而提高源代码的可读性。  这些较短的字符串将在编译时串联成一个字符串。  无论涉及到多少个字符串，都不会有运行时性能开销。  
  
 [!code-cs[csProgGuideStrings#30](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#30)]  
  
## 示例  
 若要串联字符串变量，可以使用 `+` 或 `+=` 运算符，也可以使用 <xref:System.String.Concat%2A?displayProperty=fullName>、<xref:System.String.Format%2A?displayProperty=fullName> 或 <xref:System.Text.StringBuilder.Append%2A?displayProperty=fullName> 方法。  `+` 运算符容易使用，且有利于提高代码的直观性。  即使在一条语句中使用多个 \+ 运算符，字符串内容也将只复制一次。  但是，如果重复此操作多次（如使用循环），则可能会导致出现效率问题。  例如，考虑下面的代码：  
  
 [!code-cs[csProgGuideStrings#23](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#23)]  
  
> [!NOTE]
>  在字符串串联操作中，C\# 编译器对 null 字符串和空字符串进行相同的处理，但它不转换原始 null 字符串的值。  
  
 如果您串联的字符串数量不那么巨大（例如，在循环中），那么这些代码的性能成本可能不会很高。  上述情况同样适用于 <xref:System.String.Concat%2A?displayProperty=fullName> 和 <xref:System.String.Format%2A?displayProperty=fullName> 方法。  
  
 但如果性能的优劣很重要，则应该总是使用 <xref:System.Text.StringBuilder> 类来串联字符串。  下面的代码使用 <xref:System.Text.StringBuilder> 类的 <xref:System.Text.StringBuilder.Append%2A> 方法来串联字符串，因此不会有 `+` 运算符的链接作用产生。  
  
 [!code-cs[csProgGuideStrings#22](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#22)]  
  
## 请参阅  
 <xref:System.String>   
 <xref:System.Text.StringBuilder>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [字符串](../../../csharp/programming-guide/strings/index.md)