---
title: "异常处理（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "异常处理 [C#], 关于异常处理"
  - "异常 [C#], 处理"
ms.assetid: b4e4ecf2-b907-4e58-891f-2563762258e9
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# 异常处理（C# 编程指南）
C\# 程序员可使用 [try](../../../csharp/language-reference/keywords/try-catch.md) 块对可能受异常影响的代码进行分区。  关联的 [catch](../../../csharp/language-reference/keywords/try-catch.md) 块用于处理任何结果异常。  一个包含代码的 [finally](../../../csharp/language-reference/keywords/try-finally.md) 块，无论 `try` 块中是否引发异常（例如，释放在 `try` 块中分配的资源），这些代码都会运行。  一个 `try` 块需要一个或多个关联的 `catch` 块或一个 `finally` 块，或两者。  
  
 以下示例给出了一个 `try-catch` 语句，一个 `try-finally` 语句，和一个  `try-catch-finally` 语句。  
  
 [!code-cs[csProgGuideExceptions#6](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_1.cs)]  
  
 [!code-cs[csProgGuideExceptions#7](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_2.cs)]  
  
 [!code-cs[csProgGuideExceptions#8](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_3.cs)]  
  
 不带有 `catch` 或 `finally` 块的 `try` 块将导致编译器错误。  
  
## Catch 块  
 `catch` 块可以指定要捕捉的异常的该类型。  类型规范称为“异常筛选器”。  异常类型应从 <xref:System.Exception> 派生出来。  一般而言，不会将 <xref:System.Exception> 指定为异常筛选器，除非您了解如何处理 `try` 块中可能引发的所有异常，或者您在 `catch` 块中包括了 [throw](../../../csharp/language-reference/keywords/throw.md) 语句。  
  
 具有不同异常筛选器的多个 `catch` 块可以串联在一起。  多个 `catch` 数据块的计算顺序是在代码中从顶部到底部，但是，对于所引发的每个异常，都只执行一个 `catch` 数据块。  与指定的准确类型或其基类最为匹配的第一个 `catch` 块被执行。  如果 `catch` 块没有指定匹配异常筛选器，则 `catch` 块就不具有选定的筛选器（如果语句有的话）。  需要将带有最具体的（即派生程度最高的）异常类的 `catch` 块放在最前面。  
  
 当下列条件为真时，应该捕捉异常：  
  
-   对引发异常的原因有具体的了解，并可实现特定的恢复，例如，在捕获 <xref:System.IO.FileNotFoundException> 对象时提示用户输入新的文件名。  
  
-   可以新建一个更具体的异常并引发该异常。  
  
     [!code-cs[csProgGuideExceptions#9](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_4.cs)]  
  
-   希望在将异常传递出去进行额外处理前部分地处理异常。  在下面的示例中，`catch` 块用于在再次引发异常之前，向错误日志添加条目。  
  
     [!code-cs[csProgGuideExceptions#10](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_5.cs)]  
  
## Finally 块  
 可以使用 `finally` 块清理在 `try` 块中执行的操作。  如果存在，`finally` 块将在最后执行，在 `try` 块和任何匹配 `catch` 的块之后执行。  不管是否引发异常或者是否找到与异常类型匹配的 `catch` 块，`finally` 始终运行。  
  
 可以使用 `finally` 块释放资源（如文件流、数据库连接和图形句柄），而不用等待由运行时中的垃圾回收器来完成对象。  有关更多信息，请参见[using 语句](../../../csharp/language-reference/keywords/using-statement.md)。  
  
 在下面的示例中，使用 `finally` 块关闭在 `try` 块中打开的文件。  注意，在关闭文件之前要检查该文件句柄的状态。  如果 `try` 块无法打开文件，则文件句柄仍具有值 `null`，并且 `finally` 块不会尝试关闭它。  或者，如果在 `try` 块中成功打开该文件，则 `finally` 块将关闭打开的文件。  
  
 [!code-cs[csProgGuideExceptions#11](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/exception-handling_6.cs)]  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try\-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try\-catch\-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)