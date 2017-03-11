---
title: "try-finally（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "finally"
  - "finally_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "finally 关键字 [C#]"
  - "try-finally 语句 [C#]"
ms.assetid: c27623fb-7261-4464-862c-7a369d3c8f0a
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# try-finally（C# 参考）
使用 `finally` 块，可以清理在 [Try](../../../csharp/language-reference/keywords/try-catch.md) 中分配的任何资源，而且，即使在 `try` 块中发生异常，您也可以运行代码。  通常，控件离开 `try` 语句之后，`finally` 的语句会阻止运行。  正常执行中 `break`、`continue`、`goto` 或 `return` 语句的执行，或对 `try` 语句外部异常的传播，可能会导致发生控件转换。  
  
 已处理的异常中会确保运行关联的 `finally` 块。  但是，如果异常未得到处理，则 `finally` 块的执行取决于如何触发异常展开操作。  此操作又取决于计算机是如何设置的。  有关更多信息，请参见 [Unhandled Exception Processing in the CLR](http://go.microsoft.com/fwlink/?LinkId=128371)（CLR 中的未经处理的异常处理）。  
  
 通常，当未经处理的异常中止应用程序时，`finally` 块是否运行并不重要。  但是，如果您拥有的 `finally` 块中的语句必须在该环境下运行，则一个解决方案是将 `catch` 块添加到 `try`\-`finally` 语句中。  或者，可以捕获可能是在调用堆栈更上方的 `try`\-`finally` 语句的 `try` 块中引发的异常。  即可以捕获调用了包含 `try`\-`finally` 语句的方法中的、或调用了该方法的方法中的、或调用堆栈中任何方法中的异常。  如果未捕获异常，则 `finally` 块的执行取决于操作系统是否选择触发异常展开操作。  
  
## 示例  
 在下面的示例中，无效转换语句导致 `System.InvalidCastException` 异常。  异常未处理。  
  
 [!code-cs[csrefKeywordsExceptions#4](../../../csharp/language-reference/keywords/codesnippet/csharp/try-finally_1.cs)]  
  
 在下面的示例中，`TryCast` 方法中的异常在延伸调用堆栈的方法中被捕获。  
  
 [!code-cs[csrefKeywordsExceptions#6](../../../csharp/language-reference/keywords/codesnippet/csharp/try-finally_2.cs)]  
  
 有关 `finally` 的更多信息，请参见 [try\-catch\-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)。  
  
 C\# 还包含[使用语句](../../../csharp/language-reference/keywords/using-statement.md)，该语句可为 <xref:System.IDisposable> 对象提供类似功能的方法语法。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [try、throw 和 catch 语句 \(C\+\+\)](/visual-cpp/cpp/try-throw-and-catch-statements-cpp)   
 [异常处理语句](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [如何：显式引发异常](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)