---
title: "Await 运算符 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Await"
helpviewer_keywords: 
  - "Await [Visual Basic]"
  - "Await 运算符 [Visual Basic]"
ms.assetid: 6b1ce283-e92b-4ba7-b081-7be7b3d37af9
caps.latest.revision: 30
caps.handback.revision: 30
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Await 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

您在异步方法或 lambda 表达式应用 `Await` 运算符用以延迟该操作直到所等待任务完成。  表示正在进行的工作的任务。  
  
 使用 `Await` 的方法必须具有 [Async](../../../visual-basic/language-reference/modifiers/async.md) 修饰符修饰。  由使用 `Async` 修饰符定义且通常包含一个或多个 `Await` 表达式的此类方法称为*异步方法*。  
  
> [!NOTE]
>  在 Visual Studio 2012 中引入 `Async` 和 `Await` 关键字。  有关异步编程的介绍，请参见 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 应用 `Await` 运算符的任务的返回值通常是调用一个[基于任务的异步模式](http://go.microsoft.com/fwlink/?LinkId=204847) 的方法，即 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>.  
  
 在以下代码中，<xref:System.Net.Http.HttpClient> 方法 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> 返回 `getContentsTask`，一个 `Task(Of Byte())`。  当操作完成时，任务约定生成一个实际字节数组。  `Await` 运算符应用于 `getContentsTask` 以挂起 `SumPageSizesAsync` 中的执行，直到 `getContentsTask` 完成。  同时，控制返回到 `SumPageSizesAsync` 的调用方。  `getContentsTask` 完成时，`Await` 表达式的计算结果为字节数组。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
> [!IMPORTANT]
>  有关完整的示例，请参见[演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  您可以在 Microsoft 网站上从[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409)中下载示例。  此示例在 AsyncWalkthrough\_HttpClient 项目中。  
  
 如果 `Await` 应用于返回一个 `Task(Of TResult)` 结果的方法调用，则 `Await` 表达式的类型为 TResult。  如果 `Await` 应用于返回 `Task`结果的方法调用，`Await` 表达式不返回值。  下面的示例演示这种差异。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 `Await` 表达式或声明不阻止正在其上执行的线程。  相反，它导致编译器将剩下的异步方法注册为 `Await` 表达式之后的相继的等待任务。  控制，然后返回至异步方法的调用方。  任务完成后会调用自身的继续，且异步方法的执行会恢复到其停止的位置。  
  
 `Await` 表达式只发生在由 `Async` 修饰符标记的一个立即封闭方法体或 lambda 表达式中。  *Await*术语在该上下文中仅用作关键字。  在其他地方，其解释为标识符。  在异步方法或 lambda 表达式中，`Await` 表达式不能在查询表达式，[try…catch…finally](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md) 语句中的 `catch` 或 `finally` 块中 ，循环控制变量表达式 `For` 或 `For Each` 的循环中，或者 [SyncLock](../../../visual-basic/language-reference/statements/synclock-statement.md) 语句的主体中出现。  
  
## 异常  
 大多数异步方法返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。  返回任务的属性承载有关其状态和历史记录的信息，例如任务是否已完成，异步方法是否引发异常或已取消，以及最终结果如何。  `Await` 运算符访问那些属性。  
  
 如果等待导致异常的任务返回的异步方法，`Await` 运算符会再次引发异常。  
  
 如果等待的返回任务的异步方法取消了，`Await` 运算符将再次引发 <xref:System.OperationCanceledException>。  
  
 处于出错状态的单个任务可能反映出多个异常。例如，该任务可能是对 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> 调用的结果。  当您等待此类任务时，await 操作只能再次引发异常中的一个。  但是，您不能预测哪些异常是重新引发的。  
  
 有关错误处理同步方法的示例，请参见 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## 示例  
 以下 Windows Forms 示例说明了异步方法 `WaitAsynchronouslyAsync` 中 `Await` 的使用。  比较此方法的行为与 `WaitSynchronously` 的行为。  如果没有应用 `Await` 运算符，`WaitSynchronously` 就会同步运行，而不管其定义中是否使用了 `Async` 修饰符和对其主体是否调用了 <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>。  
  
```vb  
Private Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
    ' Call the method that runs asynchronously.  
    Dim result As String = Await WaitAsynchronouslyAsync()  
  
    ' Call the method that runs synchronously.  
    'Dim result As String = Await WaitSynchronously()  
  
    ' Display the result.  
    TextBox1.Text &= result  
End Sub  
  
' The following method runs asynchronously. The UI thread is not  
' blocked during the delay. You can move or resize the Form1 window   
' while Task.Delay is running.  
Public Async Function WaitAsynchronouslyAsync() As Task(Of String)  
    Await Task.Delay(10000)  
    Return "Finished"  
End Function  
  
' The following method runs synchronously, despite the use of Async.  
' You cannot move or resize the Form1 window while Thread.Sleep  
' is running because the UI thread is blocked.  
Public Async Function WaitSynchronously() As Task(Of String)  
    ' Import System.Threading for the Sleep method.  
    Thread.Sleep(10000)  
    Return "Finished"  
End Function  
```  
  
## 请参阅  
 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [Async](../../../visual-basic/language-reference/modifiers/async.md)