---
title: "async（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "async_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "async [C#]"
  - "async 关键字 [C#]"
  - "async 方法 [C#]"
ms.assetid: 16f14f09-b2ce-42c7-a875-e4eca5d50674
caps.latest.revision: 52
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 52
---
# async（C# 参考）
使用 `async` 修饰符可将方法、[lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)或[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)指定为异步。  如果对方法或表达式使用此修饰符，则其称为异步方法。  
  
```c#  
public async Task<int> ExampleMethodAsync()  
{  
    // . . . .  
}  
  
```  
  
 如果你不熟悉异步编程或不了解异步方法如何使用 `await` 关键字来完成可能需要长时间运行的工作而不阻止调用方的线程，则应阅读[使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)中的简介。  
  
```  
string contents = await contentsTask;  
```  
  
 方法将同步运行，直至到达其第一个 `await` 表达式，此时会将方法挂起，直到等待的任务完成。  同时，如下节示例中所示，控件将返回到方法的调用方。  
  
 如果 `async` 关键字修改的方法不包含 `await` 表达式或语句，则该方法将同步执行。  编译器警告将通知你不包含 `await` 的任何异步方法，因为该情况可能表示存在错误。  请参见[编译器警告（等级 1）CS4014](../../../csharp/language-reference/compiler-messages/cs4014.md)。  
  
 `async` 关键字是上下文关键字，原因在于只有当它修饰方法、lambda 表达式或匿名方法时，它才是关键字。  在所有其他上下文中，都会将其解释为标识符。  
  
## 示例  
 下面的示例展示了异步事件处理程序 `StartButton_Click` 和异步方法 `ExampleMethodAsync` 之间的控制结构和流程。  此异步方法得到的结果是一个下载网站的长度。  此代码适用于在 [!INCLUDE[vs_dev12](../../../csharp/getting-started/includes/vs-dev12-md.md)] 中创建的 Windows Presentation Foundation \(WPF\) 应用或 Windows 应用商店应用；请参见有关设置应用的代码注释。  
  
```c#  
// You can run this code in Visual Studio 2013 as a WPF app or a Windows Store app.  
// You need a button (StartButton) and a textbox (ResultsTextBox).  
// Remember to set the names and handler so that you have something like this:  
// <Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"  
//         Click="StartButton_Click" Name="StartButton"/>  
// <TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"   
//          Text="TextBox" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>  
  
// To run the code as a WPF app:  
//    paste this code into the MainWindow class in MainWindow.xaml.cs,  
//    add a reference to System.Net.Http, and  
//    add a using directive for System.Net.Http.  
  
// To run the code as a Windows Store app:  
//    paste this code into the MainPage class in MainPage.xaml.cs, and  
//    add using directives for System.Net.Http and System.Threading.Tasks.  
  
private async void StartButton_Click(object sender, RoutedEventArgs e)  
{  
    // ExampleMethodAsync returns a Task<int>, which means that the method  
    // eventually produces an int result. However, ExampleMethodAsync returns  
    // the Task<int> value as soon as it reaches an await.  
    ResultsTextBox.Text += "\n";  
    try  
    {  
        int length = await ExampleMethodAsync();  
        // Note that you could put "await ExampleMethodAsync()" in the next line where  
        // "length" is, but due to when '+=' fetches the value of ResultsTextBox, you  
        // would not see the global side effect of ExampleMethodAsync setting the text.  
        ResultsTextBox.Text += String.Format("Length: {0}\n", length);  
    }  
    catch (Exception)  
    {  
        // Process the exception if one occurs.  
    }  
}  
  
public async Task<int> ExampleMethodAsync()  
{  
    var httpClient = new HttpClient();  
    int exampleInt = (await httpClient.GetStringAsync("http://msdn.microsoft.com")).Length;  
    ResultsTextBox.Text += "Preparing to finish ExampleMethodAsync.\n";  
    // After the following return statement, any method that's awaiting  
    // ExampleMethodAsync (in this case, StartButton_Click) can get the   
    // integer result.  
    return exampleInt;  
}  
// Output:  
// Preparing to finish ExampleMethodAsync.  
// Length: 53292  
  
```  
  
> [!IMPORTANT]
>  有关各项任务以及在等待任务期间所执行代码的更多信息，请参见[使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。有关使用类似元素的完整 WPF 示例，请参见[演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  你可以从[开发人员代码示例](http://go.microsoft.com/fwlink/?LinkId=255191)下载演练代码。  
  
## 返回类型  
 异步方法的返回类型可以为 <xref:System.Threading.Tasks.Task>、<xref:System.Threading.Tasks.Task%601> 或 [void](../../../csharp/language-reference/keywords/void.md)。  方法不能声明任何 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 参数，但是可以调用具有这类参数的方法。  
  
 如果异步方法的[返回](../../../csharp/language-reference/keywords/return.md)语句指定一个 `TResult` 类型的操作数，则你应指定 `Task<TResult>` 作为方法的返回类型。  如果当方法完成时未返回有意义的值，则应使用 `Task`。  即，对方法的调用将返回一个 `Task`，但是当 `Task` 完成时，任何等待 `Task` 的所有 `await` 表达式的计算结果都为 `void`。  
  
 你应主要使用 `void` 返回类型来定义事件处理程序，这些处理程序需要此返回类型。  `void` 返回异步方法的调用方不能等待，并且无法捕获该方法引发的异常。  
  
 有关更多信息和示例，请参见[异步返回类型](../Topic/Async%20Return%20Types%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 请参阅  
 <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>   
 [await](../../../csharp/language-reference/keywords/await.md)   
 [演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)