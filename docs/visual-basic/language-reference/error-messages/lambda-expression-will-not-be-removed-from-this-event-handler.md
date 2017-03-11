---
title: "将不会从此事件处理程序中移除 Lambda 表达式 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc42326"
  - "vbc42326"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42326"
ms.assetid: 63214dc6-0112-4245-8ebf-7c9e8f5a5782
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 将不会从此事件处理程序中移除 Lambda 表达式
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将不会从此事件处理程序中移除 Lambda 表达式。请将该 lambda 表达式赋给一个变量，并使用该变量来添加和移除事件。  
  
 在将 lambda 表达式与事件处理程序一起使用时，可能看不到预期的行为。  即使每个 lambda 表达式定义都完全相同，编译器也会为它们分别生成一个新的方法。  因此，下面的代码显示 `False`。  
  
```vb#  
Module Module1  
  
    Sub Main()  
        Dim fun1 As ChangeInteger = Function(p As Integer) p + 1  
        Dim fun2 As ChangeInteger = Function(p As Integer) p + 1  
        Console.WriteLine(fun1 = fun2)  
    End Sub  
  
    Delegate Function ChangeInteger(ByVal x As Integer) As Integer  
  
End Module  
```  
  
 在将 lambda 表达式与事件处理程序一起使用时，这可能导致意外结果。  在下面的示例中，由 `AddHandler` 添加的 lambda 表达式未被 `RemoveHandler` 语句移除。  
  
```vb#  
Module Module1  
  
    Event ProcessInteger(ByVal x As Integer)  
  
    Sub Main()  
  
        ' The following line adds one listener to the event.  
        AddHandler ProcessInteger, Function(m As Integer) m  
  
        ' The following statement searches the current listeners   
        ' for a match to remove. However, this lambda is not the same  
        ' as the previous one, so nothing is removed.  
        RemoveHandler ProcessInteger, Function(m As Integer) m  
  
    End Sub  
End Module  
```  
  
 默认情况下，此消息是一个警告。  有关如何隐藏警告或将警告视为错误的更多信息，请参见[在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42326  
  
### 更正此错误  
  
-   若要避免警告并移除 lambda 表达式，请将 lambda 表达式赋给一个变量，并在 `AddHandler` 和 `RemoveHandler` 语句中都使用该变量，如下面的示例所示。  
  
    ```vb#  
    Module Module1  
  
        Event ProcessInteger(ByVal x As Integer)  
  
        Dim PrintHandler As ProcessIntegerEventHandler  
  
        Sub Main()  
  
            ' Assign the lambda expression to a variable.  
            PrintHandler = Function(m As Integer) m  
  
            ' Use the variable to add the listener.  
            AddHandler ProcessInteger, PrintHandler  
  
            ' Use the variable again when you want to remove the listener.  
            RemoveHandler ProcessInteger, PrintHandler  
  
        End Sub  
    End Module  
    ```  
  
## 请参阅  
 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/events.md)