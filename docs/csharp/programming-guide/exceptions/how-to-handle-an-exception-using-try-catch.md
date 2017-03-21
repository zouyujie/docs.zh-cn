---
title: "如何：使用 try/catch 处理异常（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "异常处理 [C#], try/catch 块"
  - "异常 [C#], try/catch 块"
  - "try/catch 块 [C#]"
ms.assetid: ca8e3773-980e-4767-8633-7408540e9818
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# 如何：使用 try/catch 处理异常（C# 编程指南）
[try\-catch](../../../csharp/language-reference/keywords/try-catch.md) 块的用途是捕捉和处理工作代码所生成的异常。  有些异常可以在 `catch` 块中处理，解决问题后不会再次引发异常；但更多情况下，您唯一能做的是确保引发适当的异常。  
  
## 示例  
 在此示例中，<xref:System.IndexOutOfRangeException> 不是最适当的异常：对本方法而言 <xref:System.ArgumentOutOfRangeException> 更恰当些，因为错误是由调用方传入的 `index` 参数导致的。  
  
 [!code-cs[csProgGuideExceptions#5](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-handle-an-exception-using-try-catch_1.cs)]  
  
## 注释  
 导致异常的代码被括在 `try` 块中。  在其后面紧接着添加一个 `catch` 语句，以便在 `IndexOutOfRangeException` 发生时对其进行处理。  `catch` 块处理 `IndexOutOfRangeException`，并引发更适当的 `ArgumentOutOfRangeException` 异常。  为给调用方提供尽可能多的信息，应考虑将原始异常指定为新异常的 <xref:System.Exception.InnerException%2A>。  因为 <xref:System.Exception.InnerException%2A> 属性是[只读](../../../csharp/language-reference/keywords/readonly.md)，所以必须在新异常的构造函数中为其赋值。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [异常处理](../../../csharp/programming-guide/exceptions/exception-handling.md)