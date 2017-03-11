---
title: "Async (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Async"
helpviewer_keywords: 
  - "Async [Visual Basic]"
  - "Async 关键字 [Visual Basic]"
ms.assetid: 1be8b4b5-9689-41b5-bd33-b906bfd53bc5
caps.latest.revision: 37
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 37
---
# Async (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`Async` 修饰符指示它修饰的方法或 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md) 是异步的。  此类方法称为 *异步方法*。  
  
 异步方法提供了一种简便方式完成可能需要长时间运行的工作，而不必阻止调用方的线程。  异步方法的调用方可以继续工作，而不必等待异步方法完成。  
  
> [!NOTE]
>  在 Visual Studio 2012 中引入 `Async` 和 `Await` 关键字。  有关异步编程的介绍，请参见 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 下面的示例演示了异步方法的结构。  按照约定，异步方法名的结尾为“Async "。  
  
```vb  
  
Public Async Function ExampleMethodAsync() As Task(Of Integer)  
    ' . . .  
  
    ' At the Await expression, execution in this method is suspended and,  
    ' if AwaitedProcessAsync has not already finished, control returns  
    ' to the caller of ExampleMethodAsync. When the awaited task is   
    ' completed, this method resumes execution.   
    Dim exampleInt As Integer = Await AwaitedProcessAsync()  
  
    ' . . .  
  
    ' The return statement completes the task. Any method that is   
    ' awaiting ExampleMethodAsync can now get the integer result.  
    Return exampleInt  
End Function  
```  
  
 通常，`Async` 关键字修饰的方法至少包含一个 [await](../../../visual-basic/language-reference/modifiers/async.md) 表达式或语句。  方法同步运行，直到到达第一个 `Await`，此时暂停，直到等待任务完成。  同时，控件返回至方法的调用方。  如果方法不包含一个 `Await` 表达式或语句，方法不会像同步方法一样挂起并执行。  编译器警告通知您不包含 `Await` 的任何异步方法，因为该情况可能指示错误。  有关详细信息，请参见[编译错误](../../../visual-basic/language-reference/error-messages/because-this-call-is-not-awaited-the-current-method-continues-to-run.md) “ 。  
  
 `Async` 关键字是一个非保留的关键字。  在修饰方法或 lambda 表达式时，它是关键字。  在所有其他上下文中，它解释为标识符。  
  
## 返回类型  
 异步方法是 [子](../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 程序或具有 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>的一个返回类型的 [函数](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md) 程序。  该方法不能声明任何 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) 参数。  
  
 如果一个异步方法的 [返回](../../../visual-basic/language-reference/statements/return-statement.md) 语句指定一个 TResult 类型操作数，则您必须指定 `Task(Of TResult)` 作为该异步方法的返回类型。  如果当方法完成时未返回有意义的值，则使用 `Task`。  即对方法的调用返回 `Task`，但是，随着 `Task` 完成时，等待 `Task` 的任何 `Await` 语句不会产生一个结果值。  
  
 异步子例程主要用于定义需要 `Sub` 程序的事件处理程序。  异步子程序的调用者不能等待，并且无法捕获该方法引发的异常。  
  
 有关更多信息和示例，请参见[异步返回类型](../Topic/Async%20Return%20Types%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 示例  
 下面的示例演示一个异步事件处理程序、一个异步 lambda 表达式和一个异步方法。  有关使用这些元素的完整示例，请参见 [演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  可以从[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=255191)下载演练中的代码。  
  
```vb  
  
' An event handler must be a Sub procedure.  
Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click  
    textBox1.Clear()  
    ' SumPageSizesAsync is a method that returns a Task.  
    Await SumPageSizesAsync()  
    textBox1.Text = vbCrLf & "Control returned to button1_Click."  
End Sub  
  
' The following async lambda expression creates an equivalent anonymous  
' event handler.  
AddHandler button1.Click, Async Sub(sender, e)  
                              textBox1.Clear()  
                              ' SumPageSizesAsync is a method that returns a Task.  
                              Await SumPageSizesAsync()  
                              textBox1.Text = vbCrLf & "Control returned to button1_Click."  
                          End Sub  
  
' The following async method returns a Task(Of T).  
' A typical call awaits the Byte array result:  
'      Dim result As Byte() = Await GetURLContents("http://msdn.com")  
Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
  
    ' The downloaded resource ends up in the variable named content.  
    Dim content = New MemoryStream()  
  
    ' Initialize an HttpWebRequest for the current URL.  
    Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
    ' Send the request to the Internet resource and wait for  
    ' the response.  
    Using response As WebResponse = Await webReq.GetResponseAsync()  
        ' Get the data stream that is associated with the specified URL.  
        Using responseStream As Stream = response.GetResponseStream()  
            ' Read the bytes in responseStream and copy them to content.    
            ' CopyToAsync returns a Task, not a Task<T>.  
            Await responseStream.CopyToAsync(content)  
        End Using  
    End Using  
  
    ' Return the result as a byte array.  
    Return content.ToArray()  
End Function  
  
```  
  
## 请参阅  
 <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>   
 [Await 运算符](../../../visual-basic/language-reference/operators/await-operator.md)   
 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)