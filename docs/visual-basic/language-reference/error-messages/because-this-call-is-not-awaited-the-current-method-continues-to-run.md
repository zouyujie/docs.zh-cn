---
title: "由于不等待此调用，因此在调用完成之前，当前方法将继续运行 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc42358"
  - "vbc42358"
helpviewer_keywords: 
  - "BC42358"
ms.assetid: 43342515-c3c8-4155-9263-c302afabcbc2
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 由于不等待此调用，因此在调用完成之前，当前方法将继续运行
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在调用完成之前，会继续执行当前方法，原因是此调用不处于等待状态。 请考虑向调用结果应用“Await”运算符。  
  
 当前方法调用返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 的异步方法，而不对结果应用 [Await](../../../visual-basic/language-reference/operators/await-operator.md) 运算符。 对异步方法的调用会启动异步任务。 但是，由于没有应用 `Await` 运算符，程序将继续运行，而不必等待任务完成。 在大多数情况下，此行为并不是你所期望的。 方法调用的其他方面通常取决于调用的结果，而调用的方法至少应在从包含调用的方法返回之前完成。  
  
 对于被调用的异步方法中引发的异常，如何进行处理同样是一个重要的问题。 在返回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 的方法中引发的异常将存储在返回的任务中。 如果不等待任务或不显式检查异常，该异常会丢失。 如果等待任务，将重新引发异常。  
  
 作为最佳做法，应始终等待调用。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的详细信息，请参阅 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42358  
  
### 解决此警告  
  
-   只有当您确定不需要等待异步调用完成并且调用的方法不会引发任何异常时，才应考虑禁止显示警告。 在此情况下，可以通过将调用的任务结果分配给变量来禁止显示警告。  
  
     下面的示例演示如何生成警告，如何禁止显示警告以及如何等待调用。  
  
    ```vb  
    Async Function CallingMethodAsync() As Task  
  
        ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
        ' Variable delay is used to slow down the called method so that you  
        ' can distinguish between awaiting and not awaiting in the program's output.   
        ' You can adjust the value to produce the output that this topic shows   
        ' after the code.  
        Dim delay = 5000  
  
        ' Call #1.  
        ' Call an async method. Because you don't await it, its completion isn't   
        ' coordinated with the current method, CallingMethodAsync.  
        ' The following line causes the warning.  
        CalledMethodAsync(delay)  
  
        ' Call #2.  
        ' To suppress the warning without awaiting, you can assign the   
        ' returned task to a variable. The assignment doesn't change how  
        ' the program runs. However, the recommended practice is always to  
        ' await a call to an async method.  
        ' Replace Call #1 with the following line.  
        'Task delayTask = CalledMethodAsync(delay)  
  
        ' Call #3  
        ' To contrast with an awaited call, replace the unawaited call   
        ' (Call #1 or Call #2) with the following awaited call. The best   
        ' practice is to await the call.  
  
        'Await CalledMethodAsync(delay)  
  
        ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
        ' continues to run and, in this example, finishes its work and returns  
        ' to its caller.  
        ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
    End Function  
  
    Async Function CalledMethodAsync(howLong As Integer) As Task  
  
        ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
        ' Slow the process down a little so you can distinguish between awaiting  
        ' and not awaiting. Adjust the value for howLong if necessary.  
        Await Task.Delay(howLong)  
        ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
    End Function  
  
    ```  
  
     在此示例中，如果选择调用 1 或调用 2，未等待的异步方法 \(`CalledMethodAsync`\) 将在调用方 \(`CallingMethodAsync`\) 和调用方的调用方 \(`StartButton_Click`\) 完成后完成。 以下输出的最后一行演示了调用的方法何时完成。 输出内容标示了整个示例中何时进入和退出调用 `CallingMethodAsync` 的事件处理程序。  
  
    ```  
  
    Entering the Click event handler.  
      Entering calling method.  
        Entering called method, starting and awaiting Task.Delay.  
      Returning from calling method.  
    Exiting the Click event handler.  
        Task.Delay is finished--returning from called method.  
    ```  
  
## 示例  
 以下 Windows Presentation Foundation \(WPF\) 应用程序包含上一示例中的方法。 下列步骤用于设置该应用程序。  
  
1.  创建一个 WPF 应用程序，将其命名为 `AsyncWarning`。  
  
2.  在 Visual Studio 代码编辑器中，选择**“MainWindow.xaml”**选项卡。  
  
     如果此选项卡不可见，则在解决方案资源管理器中，打开 MainWindow.xaml 的快捷菜单，然后选择“查看代码”。  
  
3.  在“XAML”视图中，将 MainWindow.xaml 的代码替换为下面的代码。  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="StartButton_Click" />  
            <TextBox x:Name="ResultsTextBox" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
        </Grid>  
    </Window>  
  
    ```  
  
     MainWindow.xaml 的“设计”视图中将显示一个简单的窗口，其中包含一个按钮和一个文本框。  
  
     有关 XAML 设计器的详细信息，请参阅[使用 XAML 设计器创建 UI](/visual-studio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio)。 有关如何自行生成简单 UI 的信息，请参阅[演练：使用 Async 和 Await 访问 Web](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)的“创建 WPF 应用程序的步骤”和“设计简单的 WPF MainWindow 的步骤”两个章节。  
  
4.  将 MainWindow.xaml.vb 中的代码替换为以下代码。  
  
    ```vb  
  
    Class MainWindow   
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
            ResultsTextBox.Text &= vbCrLf & "Entering the Click event handler."  
            Await CallingMethodAsync()  
            ResultsTextBox.Text &= vbCrLf & "Exiting the Click event handler."  
        End Sub  
  
        Async Function CallingMethodAsync() As Task  
  
            ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
            ' Variable delay is used to slow down the called method so that you  
            ' can distinguish between awaiting and not awaiting in the program's output.   
            ' You can adjust the value to produce the output that this topic shows   
            ' after the code.  
            Dim delay = 5000  
  
            ' Call #1.  
            ' Call an async method. Because you don't await it, its completion isn't   
            ' coordinated with the current method, CallingMethodAsync.  
            ' The following line causes the warning.  
            CalledMethodAsync(delay)  
  
            ' Call #2.  
            ' To suppress the warning without awaiting, you can assign the   
            ' returned task to a variable. The assignment doesn't change how  
            ' the program runs. However, the recommended practice is always to  
            ' await a call to an async method.  
  
            ' Replace Call #1 with the following line.  
            'Task delayTask = CalledMethodAsync(delay)  
  
            ' Call #3  
            ' To contrast with an awaited call, replace the unawaited call   
            ' (Call #1 or Call #2) with the following awaited call. The best   
            ' practice is to await the call.  
  
            'Await CalledMethodAsync(delay)  
  
            ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
            ' continues to run and, in this example, finishes its work and returns  
            ' to its caller.  
            ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
        End Function  
  
        Async Function CalledMethodAsync(howLong As Integer) As Task  
  
            ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
            ' Slow the process down a little so you can distinguish between awaiting  
            ' and not awaiting. Adjust the value for howLong if necessary.  
            Await Task.Delay(howLong)  
            ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
        End Function  
  
    End Class  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    '     Task.Delay is finished--returning from called method.  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '     Task.Delay is finished--returning from called method.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    ```  
  
5.  按 F5 键以运行程序，然后选择**“启动”**按钮。  
  
     预期的输出显示在代码末尾。  
  
## 请参阅  
 [Await 运算符](../../../visual-basic/language-reference/operators/await-operator.md)   
 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)