---
title: "如何：使用 finally 执行清理代码（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "异常处理 [C#], try/finally 块"
  - "异常 [C#], try/finally 块"
  - "try/finally 块 [C#]"
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：使用 finally 执行清理代码（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`finally` 语句的目的是确保即使在引发异常的情况下也能立即进行必要的对象（通常是保存外部资源的对象）清理。  此类清理功能的一个示例是在使用后立即对 <xref:System.IO.FileStream> 调用 <xref:System.IO.Stream.Close%2A>，而不是等待公共语言运行时对该对象进行垃圾回收，如下所示：  
  
 [!code-cs[csProgGuideExceptions#16](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_1.cs)]  
  
## 示例  
 为了将上面的代码转换为 `try-catch-finally` 语句，需要将清理代码与工作代码分开，如下所示。  
  
 [!code-cs[csProgGuideExceptions#17](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_2.cs)]  
  
 因为在 `OpenWrite()` 调用前，`try` 块内随时都有可能发生异常，`OpenWrite()` 调用本身也有可能失败，所以我们无法保证该文件在我们尝试关闭它时处于打开状态。  `finally` 块添加了一项检查，以确保在调用 <xref:System.IO.Stream.Close%2A> 方法前，<xref:System.IO.FileStream> 对象不为 `null`。  如果没有 `null` 检查，`finally` 块可能引发自身的 <xref:System.NullReferenceException>，但是应当尽可能避免在 `finally` 块中引发异常。  
  
 在 `finally` 块中关闭数据库连接是另一个不错的选择。  因为有时候数据库服务器允许的连接数是有限的，所以应尽快关闭数据库连接。  在由于引发了异常而无法关闭连接的情况下，使用 `finally` 块也是比等待垃圾回收更好的一种选择。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [异常处理](../../../csharp/programming-guide/exceptions/exception-handling.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try\-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try\-catch\-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)