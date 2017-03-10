---
redirect_url: /dotnet/articles/csharp/programming-guide/exceptions/
caps.handback.revision: 33
---
# 异常和异常处理（C# 编程指南）
C\# 语言的异常处理功能可帮助您处理程序运行时出现的任何意外或异常情况。  异常处理使用 `try`、`catch` 和 `finally` 关键字尝试某些操作，以处理失败情况，尽管这些操作有可能失败，但如果您确定需要这样做，且希望在事后清理资源，就可以尝试这样做。  公共语言运行时 \(CLR\)、.NET Framework 或任何第三方库或者应用程序代码都可以生成异常。  异常是使用 `throw` 关键字创建的。  
  
 很多情况下，异常可能不是由代码直接调用的方法引发，而是由调用堆栈中位置更靠下的另一个方法所引发。  在这种情况下，CLR 将展开堆栈，查找是否有方法包含针对该特定异常类型的 `catch` 块，如果找到这样的方法，就会执行找到的第一个这样的 `catch` 块。  如果在调用堆栈中的任何位置都没有找到适当的 `catch` 块，就会终止该进程，并向用户显示一条消息。  
  
 此示例中使用一个方法检测是否有被零除的情况；如果有，则捕获该错误。  如果没有异常处理，此程序将终止并产生**“DivideByZeroException 未处理”**错误。  
  
 [!code-cs[csProgGuideExceptions#18](../../../csharp/programming-guide/exceptions/codesnippet/csharp/exceptions-and-exception_1.cs)]  
  
## 异常概述  
 异常具有以下特点：  
  
-   各种类型的异常最终都是由 `System.Exception` 派生而来。  
  
-   在可能引发异常的语句周围使用 `try` 块。  
  
-   一旦 `try` 块中发生异常，控制流将跳转到第一个关联的异常处理程序（无论该处理程序存在于调用堆栈中的什么位置）。  在 C\# 中，`catch` 关键字用于定义异常处理程序。  
  
-   如果给定异常没有异常处理程序，则程序将停止执行，并显示一条错误消息。  
  
-   除非您可以处理某个异常并使应用程序处于已知状态，否则请不要捕捉该异常。  如果捕捉 `System.Exception`，请在 `catch` 块的末尾使用 `throw` 关键字再次引发该异常。  
  
-   如果 `catch` 块定义了一个异常变量，则可以用它获取有关所发生异常类型的更多信息。  
  
-   程序可以使用 `throw` 关键字显式地引发异常。  
  
-   异常对象包含有关错误的详细信息，比如调用堆栈的状态以及有关错误的文本说明。  
  
-   即使发生异常也会执行 `finally` 块中的代码。  使用 `finally` 块释放资源，例如，关闭在 `try` 块中打开的任何流或文件。  
  
-   .NET Framework 中的托管异常是凭借 Win32 结构化异常处理机制实现的。  有关更多信息，请参见[结构化异常处理](/visual-cpp/cpp/structured-exception-handling-c-cpp) 和 [A Crash Course on the Depths of Win32 Structured Exception Handling](http://go.microsoft.com/fwlink/?LinkId=119654)（有关深入探究 Win32 结构化异常处理的应急课程）。  
  
## 相关章节  
 有关异常和异常处理的更多信息，请参见以下主题：  
  
-   [使用异常](../../../csharp/programming-guide/exceptions/using-exceptions.md)  
  
-   [异常处理](../../../csharp/programming-guide/exceptions/exception-handling.md)  
  
-   [创建和引发异常](../../../csharp/programming-guide/exceptions/creating-and-throwing-exceptions.md)  
  
-   [编译器生成的异常](../../../csharp/programming-guide/exceptions/compiler-generated-exceptions.md)  
  
-   [如何：使用 try\/catch 处理异常](../../../csharp/programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md)  
  
-   [如何：使用 finally 执行清理代码](../../../csharp/programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.SystemException>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try\-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try\-catch\-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)   
 [异常](../Topic/Handling%20and%20Throwing%20Exceptions.md)   
 [异常层次结构](../Topic/Exception%20Hierarchy.md)   
 [编写可靠的 .NET 代码](http://go.microsoft.com/fwlink/?LinkId=112400)   
 [特定异常的 Minidumps](http://go.microsoft.com/fwlink/?LinkId=112408)