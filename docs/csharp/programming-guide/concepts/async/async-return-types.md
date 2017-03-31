---
title: "异步返回类型 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: ddb2539c-c898-48c1-ad92-245e4a996df8
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4c1bab99fc1139f03e5f754cfecaee392b947171
ms.lasthandoff: 03/13/2017

---
# <a name="async-return-types-c"></a>异步返回类型 (C#)
异步方法有三种可能的返回类型：<xref:System.Threading.Tasks.Task%601>、<xref:System.Threading.Tasks.Task> 和无效。 在 Visual Basic 中，void 返回类型被写为 [Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 过程。 有关异步方法的详细信息，请参阅[使用 Async 和 Await 的异步编程 (C#)](../../../../csharp/programming-guide/concepts/async/index.md)。  
  
 在以下其中一节检查每个返回类型，且在本主题末尾可以找到使用全部三种类型的完整示例。  
  
> [!NOTE]
>  若要运行该示例，计算机上必须安装 Visual Studio 2012 或更高版本和 .NET Framework 4.5 或更高版本。  
  
##  <a name="BKMK_TaskTReturnType"></a>Task(T) 返回类型  
 <xref:System.Threading.Tasks.Task%601> 返回类型可用于包含 [return](../../../../csharp/language-reference/keywords/return.md) (C#) 语句（其中操作数含有类型 `TResult`）的异步方法。  
  
 在下面的示例中，`TaskOfT_MethodAsync` 异步方法包含返回整数的 return 语句。 因此，该方法声明必须指定 `Task<int>` 的返回类型。  
  
```cs  
// TASK<T> EXAMPLE  
async Task<int> TaskOfT_MethodAsync()  
{  
    // The body of the method is expected to contain an awaited asynchronous  
    // call.  
    // Task.FromResult is a placeholder for actual work that returns a string.  
    var today = await Task.FromResult<string>(DateTime.Now.DayOfWeek.ToString());  
  
    // The method then can process the result in some way.  
    int leisureHours;  
    if (today.First() == 'S')  
        leisureHours = 16;  
    else  
        leisureHours = 5;  
  
    // Because the return statement specifies an operand of type int, the  
    // method must have a return type of Task<int>.  
    return leisureHours;  
}  
```  
  
 当 `TaskOfT_MethodAsync` 从 await 表达式中调用时，await 表达式将检索存储在由 `TaskOfT_MethodAsync` 返回的任务中的整数值（`leisureHours` 的值）。 有关 await 表达式的详细信息，请参阅 [await](../../../../csharp/language-reference/keywords/await.md)。  
  
 以下代码调用和等待方法 `TaskOfT_MethodAsync`。 此结果分配给 `result1` 变量。  
  
```cs  
// Call and await the Task<T>-returning async method in the same statement.  
int result1 = await TaskOfT_MethodAsync();  
```  
  
 通过从应用程序 `await` 中分离对 `TaskOfT_MethodAsync` 的调用，你可以更好地了解此操作，如下面的代码所示。 对非立即等待的方法 `TaskOfT_MethodAsync` 的调用返回 `Task<int>`，正如你从方法声明预料的一样。 该任务指派给示例中的 `integerTask` 变量。 由于 `integerTask` 是 <xref:System.Threading.Tasks.Task%601>，它包含了类型 `TResult` 的 <xref:System.Threading.Tasks.Task%601.Result> 属性。 在这种情况下，TResult 表示整数类型。 当 `await` 应用于 `integerTask` 时，await 表达式将对 `integerTask` 属性的 <xref:System.Threading.Tasks.Task%601.Result%2A> 的内容求值。 此值分配给 `result2` 变量。  
  
> [!WARNING]
>  <xref:System.Threading.Tasks.Task%601.Result%2A> 属性是堵塞属性。 如果你在其任务完成之前尝试访问它，当前处于活动状态的线程将被阻止，直到任务完成且值为可用。 在大多数情况下，应通过使用 `await` 访问此值，而不是直接访问属性。  
  
```cs  
// Call and await in separate statements.  
Task<int> integerTask = TaskOfT_MethodAsync();  
  
// You can do other work that does not rely on integerTask before awaiting.  
textBox1.Text += String.Format("Application can continue working while the Task<T> runs. . . . \r\n");  
  
int result2 = await integerTask;  
```  
  
 以下代码中的显示语句验证 `result1` 变量、`result2` 变量与 `Result` 属性的值是否相同。 请记住，`Result` 属性是锁定属性，在其任务完成之前不应访问。  
  
```cs  
// Display the values of the result1 variable, the result2 variable, and  
// the integerTask.Result property.  
textBox1.Text += String.Format("\r\nValue of result1 variable:   {0}\r\n", result1);  
textBox1.Text += String.Format("Value of result2 variable:   {0}\r\n", result2);  
textBox1.Text += String.Format("Value of integerTask.Result: {0}\r\n", integerTask.Result);  
```  
  
##  <a name="BKMK_TaskReturnType"></a>任务返回类型  
 不包含 return 语句或包含不返回操作数的 return 语句的异步方法通常具有返回类型 <xref:System.Threading.Tasks.Task>。 如果被编写为异步运行，这些方法将为返回 void 的方法。 如果在异步方法中使用 `Task` 返回类型，调用方法可以使用 await 运算符暂停调用方的完成，直至被调用的异步方法结束。  
  
 在下面的示例中，异步方法 `Task_MethodAsync` 不包含 return 语句。 因此，为此方法指定 `Task` 返回类型，这将启用 `Task_MethodAsync` 为等待。 `Task` 类型的定义不包括存储返回值的 `Result` 属性。  
  
```cs  
// TASK EXAMPLE  
async Task Task_MethodAsync()  
{  
    // The body of an async method is expected to contain an awaited   
    // asynchronous call.  
    // Task.Delay is a placeholder for actual work.  
    await Task.Delay(2000);  
    // Task.Delay delays the following line by two seconds.  
    textBox1.Text += String.Format("\r\nSorry for the delay. . . .\r\n");  
  
    // This method has no return statement, so its return type is Task.    
}  
```  
  
 通过使用 await 语句而不是 await 表达式来调用和等待 `Task_MethodAsync`，类似于同步返回 void 的方法的调用语句。 Await 运算符的应用程序在这种情况下不生成值。  
  
 以下代码调用和等待方法 `Task_MethodAsync`。  
  
```cs  
// Call and await the Task-returning async method in the same statement.  
await Task_MethodAsync();  
```  
  
 如同上个 <xref:System.Threading.Tasks.Task%601> 示例，可以从 await 运算符的应用程序中分离对 `Task_MethodAsync` 的调用，如以下代码所示。 但是，请记住，`Task` 没有 `Result` 属性，并且当 await 运算符应用于 `Task` 时不产生值。  
  
 以下代码从等待 `Task_MethodAsync` 返回的任务中分离调用 `Task_MethodAsync`。  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
##  <a name="BKMK_VoidReturnType"></a>返回类型为 void  
 Void 返回类型主要用在事件处理程序中，其中需要 void 返回类型。 Void 返回还可用于替代返回 void 的方法，或者用于执行可分类为"发后不理"活动的方法。 但是，你应尽可能地返回 `Task`，因为不能等待返回 void 的异步方法。 这种方法的任何调用方必须能够继续完成，而无需等待调用的异步方法完成，并且调用方必须独立于异步方法生成的任何值或异常。  
  
 返回 void 的异步方法的调用方无法捕获从该方法引发的异常，且此类未经处理的异常可能会导致应用程序故障。 如果返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 的异步方法中出现异常，此异常将存储于返回的任务中，并在等待该任务时再次引发。 因此，请确保可以产生异常的任何异步方法都具有返回类型 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>，并确保会等待对方法的调用。  
  
 有关如何在异步方法中捕捉异常的更多信息，请参阅 [try-catch](../../../../csharp/language-reference/keywords/try-catch.md)。  
  
 下面的代码定义了异步事件处理程序。  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
##  <a name="BKMK_Example"></a>完整的示例  
 以下 Windows Presentation Foundation (WPF) 项目包含本主题中的代码示例。  
  
 若要运行项目，请执行下列步骤：  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，依次选择“文件” ****、“新建” ****、“项目” ****。  
  
     **“新建项目”** 对话框随即打开。  
  
3.  在“模板”****类别的“已安装”****中，选择“Visual C#”，然后选择“Windows”****。 从项目类型列表中，选择“WPF 应用程序”****。  
  
4.  输入 `AsyncReturnTypes` 作为项目名称，然后选择“确定”****按钮。  
  
     新项目将出现在“解决方案资源管理器”****中。  
  
5.  在 Visual Studio 代码编辑器中，选择 **“MainWindow.xaml”** 选项卡。  
  
     如果此选项卡不可见，则在“解决方案资源管理器”****中，打开 MainWindow.xaml 的快捷菜单，然后选择“打开”****。  
  
6.  在 MainWindow.xaml 的“XAML”****窗口中，将代码替换为下面的代码。  
  
    ```cs  
    <Window x:Class="AsyncReturnTypes.MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="button1" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="button1_Click"/>  
            <TextBox x:Name="textBox1" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
  
        </Grid>  
    </Window>  
  
    ```  
  
     MainWindow.xaml 的“设计”****视图中将显示一个简单的窗口，其中包含一个文本框和一个按钮。  
  
7.  在“解决方案资源管理器”****中，打开 MainWindow.xaml.cs 的快捷菜单，然后选择“查看代码”****。  
  
8.  将 MainWindow.xaml.cs 中的代码替换为以下代码。  
  
    ```cs  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.Threading.Tasks;  
    using System.Windows;  
    using System.Windows.Controls;  
    using System.Windows.Data;  
    using System.Windows.Documents;  
    using System.Windows.Input;  
    using System.Windows.Media;  
    using System.Windows.Media.Imaging;  
    using System.Windows.Navigation;  
    using System.Windows.Shapes;  
  
    namespace AsyncReturnTypes  
    {  
        public partial class MainWindow : Window  
        {  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
  
            // VOID EXAMPLE  
            private async void button1_Click(object sender, RoutedEventArgs e)  
            {  
                textBox1.Clear();  
  
                // Start the process and await its completion. DriverAsync is a   
                // Task-returning async method.  
                await DriverAsync();  
  
                // Say goodbye.  
                textBox1.Text += "\r\nAll done, exiting button-click event handler.";  
            }  
  
            async Task DriverAsync()  
            {  
                // Task<T>   
                // Call and await the Task<T>-returning async method in the same statement.  
                int result1 = await TaskOfT_MethodAsync();  
  
                // Call and await in separate statements.  
                Task<int> integerTask = TaskOfT_MethodAsync();  
  
                // You can do other work that does not rely on integerTask before awaiting.  
                textBox1.Text += String.Format("Application can continue working while the Task<T> runs. . . . \r\n");  
  
                int result2 = await integerTask;  
  
                // Display the values of the result1 variable, the result2 variable, and  
                // the integerTask.Result property.  
                textBox1.Text += String.Format("\r\nValue of result1 variable:   {0}\r\n", result1);  
                textBox1.Text += String.Format("Value of result2 variable:   {0}\r\n", result2);  
                textBox1.Text += String.Format("Value of integerTask.Result: {0}\r\n", integerTask.Result);  
  
                // Task  
                // Call and await the Task-returning async method in the same statement.  
                await Task_MethodAsync();  
  
                // Call and await in separate statements.  
                Task simpleTask = Task_MethodAsync();  
  
                // You can do other work that does not rely on simpleTask before awaiting.  
                textBox1.Text += String.Format("\r\nApplication can continue working while the Task runs. . . .\r\n");  
  
                await simpleTask;  
            }  
  
            // TASK<T> EXAMPLE  
            async Task<int> TaskOfT_MethodAsync()  
            {  
                // The body of the method is expected to contain an awaited asynchronous  
                // call.  
                // Task.FromResult is a placeholder for actual work that returns a string.  
                var today = await Task.FromResult<string>(DateTime.Now.DayOfWeek.ToString());  
  
                // The method then can process the result in some way.  
                int leisureHours;  
                if (today.First() == 'S')  
                    leisureHours = 16;  
                else  
                    leisureHours = 5;  
  
                // Because the return statement specifies an operand of type int, the  
                // method must have a return type of Task<int>.  
                return leisureHours;  
            }  
  
            // TASK EXAMPLE  
            async Task Task_MethodAsync()  
            {  
                // The body of an async method is expected to contain an awaited   
                // asynchronous call.  
                // Task.Delay is a placeholder for actual work.  
                await Task.Delay(2000);  
                // Task.Delay delays the following line by two seconds.  
                textBox1.Text += String.Format("\r\nSorry for the delay. . . .\r\n");  
  
                // This method has no return statement, so its return type is Task.    
            }  
        }  
    }  
    ```  
  
9. 按 F5 键以运行程序，然后选择 **“启动”** 按钮。  
  
     应出现以下输出。  
  
    ```  
    Application can continue working while the Task<T> runs. . . .   
  
    Value of result1 variable:   5  
    Value of result2 variable:   5  
    Value of integerTask.Result: 5  
  
    Sorry for the delay. . . .  
  
    Application can continue working while the Task runs. . . .  
  
    Sorry for the delay. . . .  
  
    All done, exiting button-click event handler.  
    ```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Tasks.Task.FromResult%2A>   
 [演练：使用 Async 和 Await 访问 Web (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [异步程序中的控制流 (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)   
 [Async](../../../../csharp/language-reference/keywords/async.md)   
 [await](../../../../csharp/language-reference/keywords/await.md)
