---
title: "throw（C# 参考） | Microsoft Docs"
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
  - "throw"
  - "throw_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "throw 关键字 [C#]"
  - "throw 语句 [C#]"
ms.assetid: 5ac4feef-4b1a-4c61-aeb4-61d549e5dd42
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# throw（C# 参考）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`throw` 语句用于发出程序执行期间出现反常情况（异常）的信号。  
  
## 备注  
 引发的异常是一个对象，其类派生自 <xref:System.Exception?displayProperty=fullName>，如以下示例所示。  
  
```  
class MyException : System.Exception {}  
// ...  
throw new MyException();  
```  
  
 通常，`throw` 语句与 `try-catch` 或 `try-finally` 语句结合使用。可在 `catch` 块中使用 [throw](../../../csharp/language-reference/keywords/throw.md) 语句以重新引发已由 `catch` 块捕获的异常。在这种情况下，[throw](../../../csharp/language-reference/keywords/throw.md) 语句不采用异常操作数。有关更多信息和示例，请参见 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)和[如何：显式引发异常](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)。  
  
## 示例  
 此示例演示如何使用 `throw` 语句引发异常。  
  
 [!code-cs[csrefKeywordsExceptions#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/throw_1.cs)]  
  
## 代码示例  
 请参见 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)和[如何：显式引发异常](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)中的示例。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 请参阅  
 [C\# 参考](../../../visual-basic/reference/command-line-compiler/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [C\+\+ 中的 try、catch 和 throw 语句](../../../csharp/language-reference/keywords/try-catch.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [异常处理语句](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [如何：显式引发异常](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)