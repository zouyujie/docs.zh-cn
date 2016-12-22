---
title: "try-catch-finally（C# 参考） | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
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
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# try-catch-finally（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`catch` 和 `finally` 一起使用的常见方式是：在 `try` 块中获取并使用资源，在 `catch` 块中处理异常情况，并在 `finally` 块中释放资源。  
  
 有关重新引发异常的更多信息和示例，请参见 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md) 和[“引发异常”](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)。  有关 `finally` 的更多信息，请参见 [尝试最终](../../../csharp/language-reference/keywords/try-finally.md)块。  
  
## 示例  
 [!code-cs[csrefKeywordsExceptions#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch-finally_1.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [try、throw 和 catch 语句 \(C\+\+\)](/visual-cpp/cpp/try-throw-and-catch-statements-cpp)   
 [异常处理语句](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [如何：显式引发异常](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)