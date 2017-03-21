---
title: "如何：调用委托方法 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
ms.assetid: b56866ae-abf9-4a5a-a855-486359455e9c
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 如何：调用委托方法 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例演示如何将方法与委托关联然后通过委托调用该方法。  
  
### 创建委托和匹配过程  
  
1.  创建一个名为 `MySubDelegate` 的委托。  
  
    ```  
    Delegate Sub MySubDelegate(ByVal x As Integer)  
    ```  
  
2.  声明一个类，该类包含与该委托具有相同签名的方法。  
  
    ```  
    Class class1  
        Sub Sub1(ByVal x As Integer)  
            MsgBox("The value of x is: " & CStr(x))  
        End Sub  
    End Class  
    ```  
  
3.  定义一个方法，该方法创建该委托的实例并通过调用内置的 `Invoke` 方法调用与该委托关联的方法。  
  
    ```  
    Protected Sub DelegateTest()  
        Dim c1 As New class1  
        ' Create an instance of the delegate.  
        Dim msd As MySubDelegate = AddressOf c1.Sub1  
        ' Call the method.  
        msd.Invoke(10)  
    End Sub  
    ```  
  
## 请参阅  
 [Delegate 语句](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)   
 [多线程应用程序](../Topic/Multithreaded%20Applications%20\(C%23%20and%20Visual%20Basic\).md)