---
title: "await（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "await_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "await [C#]"
  - "await 关键字 [C#]"
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
caps.latest.revision: 36
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 36
---
# await（C# 参考）
`await` 运算符在异步方法应用于任务，以挂起执行方法，直到所等待的任务完成。  任务表示正在进行的工作。  
  
 在其中使用 `await` 的异步方法必须通过 [async](../../../csharp/language-reference/keywords/async.md) 关键字进行修改。  使用 `async` 修饰符定义并且通常包含一个或多个 `await` 表达式的这类方法称为*异步方法*。  
  
> [!NOTE]
>  `async` 和 `await` 关键字是在 Visual Studio 2012 中引入的。  有关异步编程的说明，请参阅[使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 应用 `await` 运算符的任务通常是实现[基于任务的异步模式](http://go.microsoft.com/fwlink/?LinkId=204847)的方法调用的返回值。  示例包括 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 类型的值。  
  
 在以下代码中，<xref:System.Net.Http.HttpClient> 方法 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> 返回 `Task\<byte[]>` \(`getContentsTask`\)。  当任务完成时，任务约定生成实际字节数组。  `await` 运算符应用于 `getContentsTask` 以在 `SumPageSizesAsync` 中挂起执行，直到 `getContentsTask` 完成。  同时，控制权会返回给 `SumPageSizesAsync` 的调用方。  当 `getContentsTask` 完成之后，`await` 表达式计算为字节数组。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
> [!IMPORTANT]
>  有关完整示例，请参阅[演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  可以从 Microsoft 网站上的[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409)下载该示例。  该示例处于 AsyncWalkthrough\_HttpClient 项目中。  
  
 如前面的示例中所示，如果 `await` 应用于返回 `Task<TResult>` 的方法调用结果，则 `await` 表达式的类型为 TResult。  如果 `await` 应用于返回 `Task` 的方法调用结果，则 `await` 表达式的类型为 void。  以下示例演示了差异。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 `await` 表达式不阻止正在执行它的线程。  而是使编译器将剩下的异步方法注册为等待任务的延续任务。  控制权随后会返回给异步方法的调用方。  任务完成时，它会调用其延续任务，异步方法的执行会在暂停的位置处恢复。  
  
 `await` 表达式只能在由 `async` 修饰符标记的立即封闭方法体、lambda 表达式或异步方法中出现。  术语*“await”*在该上下文中仅用作关键字。  在其他位置，它会解释为标识符。  在方法、lambda 表达式或匿名方法中，`await` 表达式不能在同步函数体、查询表达式、[lock 语句](../../../csharp/language-reference/keywords/lock-statement.md)块或[不安全](../../../csharp/language-reference/keywords/unsafe.md)上下文中出现。  
  
## 异常  
 大多数异步方法返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。  返回任务的属性携带有关其状态和历史记录的信息，如任务是否完成、异步方法是否导致异常或已取消以及最终结果是什么。  `await` 运算符可访问这些属性。  
  
 如果等待的任务返回异步方法导致异常，则 `await` 运算符会重新引发异常。  
  
 如果等待的任务返回异步方法取消，则 `await` 运算符会重新引发 <xref:System.OperationCanceledException>。  
  
 处于故障状态的单个任务可以反映多个异常。  例如，任务可能是对 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> 调用的结果。  等待此类任务时，等待操作仅重新引发异常之一。  但是，无法预测重新引发的异常。  
  
 有关异步方法中的错误处理的示例，请参阅 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)。  
  
## 示例  
 下面的 Windows 窗体示例阐释如何在异步方法 `WaitAsynchronouslyAsync` 中使用 `await`。  将该方法的行为与 `WaitSynchronously` 的行为进行对比。  如果未向任务应用 `await` 运算符，`WaitSynchronously` 就会同步运行，而不管其定义中是否使用了 `async` 修饰符和在主体中是否调用了 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>。  
  
```c#  
  
private async void button1_Click(object sender, EventArgs e)  
{  
    // Call the method that runs asynchronously.  
    string result = await WaitAsynchronouslyAsync();  
  
    // Call the method that runs synchronously.  
    //string result = await WaitSynchronously ();  
  
    // Display the result.  
    textBox1.Text += result;  
}  
  
// The following method runs asynchronously. The UI thread is not  
// blocked during the delay. You can move or resize the Form1 window   
// while Task.Delay is running.  
public async Task<string> WaitAsynchronouslyAsync()  
{  
    await Task.Delay(10000);  
    return "Finished";  
}  
  
// The following method runs synchronously, despite the use of async.  
// You cannot move or resize the Form1 window while Thread.Sleep  
// is running because the UI thread is blocked.  
public async Task<string> WaitSynchronously()  
{  
    // Add a using directive for System.Threading.  
    Thread.Sleep(10000);  
    return "Finished";  
}  
```  
  
## 请参阅  
 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [异步](../../../csharp/language-reference/keywords/async.md)