---
title: "在 lambda 表达式中使用迭代变量可能会产生意外的结果 | Microsoft Docs"
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
  - "vbc42324"
  - "bc42324"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42324"
ms.assetid: b5c2c4bd-3b2a-4a73-aaeb-55728eb03b68
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 在 lambda 表达式中使用迭代变量可能会产生意外的结果
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 lambda 表达式中使用迭代变量可能会产生意外的结果。应改为在循环内部创建一个局部变量并将迭代变量的值赋给它。  
  
 当您在循环内声明的 lambda 表达式中使用循环迭代变量时，将显示此警告。  例如，下面的示例导致显示此警告。  
  
```vb#  
For i As Integer = 1 To 10  
    ' The warning is given for the use of i.  
    Dim exampleFunc As Func(Of Integer) = Function() i  
Next  
```  
  
 下面的示例演示可能发生的意外结果。  
  
```vb#  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            array1(i) = Function() i  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
 `For` 循环创建一个 lambda 表达式数组，其中每个表达式都返回循环迭代变量 `i` 的值。  在 `For Each` 循环中计算 lambda 表达式时，您可能希望看到显示 0、1、2、3 和 4，即 `For` 循环中的 `i` 的连续值。  但实际上看到的却是 `i` 的最终值显示了五次：  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的更多信息，请参见[在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42324  
  
### 更正此错误  
  
-   将迭代变量的值赋给一个局部变量，并在 lambda 表达式中使用该局部变量。  
  
    ```vb#  
    Module Module1  
        Sub Main()  
            Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
            For i As Integer = 0 To 4  
                Dim j = i  
                array1(i) = Function() j  
            Next  
  
            For Each funcElement In array1  
                System.Console.WriteLine(funcElement())  
            Next  
  
        End Sub  
    End Module  
    ```  
  
## 请参阅  
 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)