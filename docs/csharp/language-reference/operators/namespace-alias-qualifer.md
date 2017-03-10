---
title: ":: 运算符（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "::_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ":: 运算符 [C#]"
  - "命名空间别名限定符运算符 (::) [C#]"
  - "命名空间 [C#], :: 运算符"
ms.assetid: 698b5a73-85cf-4e0e-9e8e-6496887f8527
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# :: 运算符（C# 参考）
命名空间别名限定符 \(`::`\) 用于查找标识符。  它通常放置在两个标识符之间，例如：  
  
 [!code-cs[csRefOperators#27](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#27)]  
  
## 备注  
 命名空间别名限定符可以是 `global`。  这将调用全局命名空间中的查找，而不是在别名命名空间中。  
  
## 更多信息  
 有关如何使用 `::` 运算符的示例，请参见下面的章节：  
  
-   [如何：使用全局命名空间别名](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 运算符](../../../csharp/language-reference/operators/index.md)   
 [命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [. 运算符](../../../csharp/language-reference/operators/member-access-operator.md)   
 [外部别名](../../../csharp/language-reference/keywords/extern-alias.md)