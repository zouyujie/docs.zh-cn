---
title: "try-catch-finally（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "catch-finally_CSharpKeyword"
  - "catch-finally"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "finally 块 [C#]"
  - "try-catch 语句 [C#]"
ms.assetid: a1b443b0-ff7a-43ab-b835-0cc9bfbd15ca
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# try-catch-finally（C# 参考）
`catch` 和 `finally` 一起使用的常见方式是：在 `try` 块中获取并使用资源，在 `catch` 块中处理异常情况，并在 `finally` 块中释放资源。  
  
 有关重新引发异常的更多信息和示例，请参见 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md) 和[“引发异常”](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)。  有关 `finally` 的更多信息，请参见 [尝试最终](../../../csharp/language-reference/keywords/try-finally.md)块。  
  
## 示例  
 [!code-cs[csrefKeywordsExceptions#1](../../../csharp/language-reference/keywords/codesnippet/csharp/try-catch-finally_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [try、throw 和 catch 语句 \(C\+\+\)](/visual-cpp/cpp/try-throw-and-catch-statements-cpp)   
 [异常处理语句](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [如何：显式引发异常](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)