---
title: "return（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "return_CSharpKeyword"
  - "return"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "return 关键字 [C#]"
  - "return 语句 [C#]"
ms.assetid: 6da6e152-5b58-4448-8f3f-470dd0617ecd
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# return（C# 参考）
`return` 语句终止它出现在其中的方法的执行并将控制返回给调用方法。  它还可以返回一个可选值。  如果方法为 `void` 类型，则可以省略 `return` 语句。  
  
 如果 return 语句位于 `try` 块中，则将在控制流返回到调用方法之前执行 `finally` 块（如果存在）。  
  
## 示例  
 在下面的示例中，方法 `A()` 以 [double](../../../csharp/language-reference/keywords/double.md) 值的形式返回变量 `Area`。  
  
 [!code-cs[csrefKeywordsJump#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/return_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [return 语句](/visual-cpp/cpp/return-statement-cpp)   
 [跳转语句](../../../csharp/language-reference/keywords/jump-statements.md)