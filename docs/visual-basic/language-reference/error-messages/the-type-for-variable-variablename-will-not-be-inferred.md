---
title: "无法推断出变量“&lt;variablename&gt;”的类型，因为它绑定到封闭范围中的某个字段 | Microsoft Docs"
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
  - "vbc42110"
  - "bc42110"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42110"
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
caps.latest.revision: 33
caps.handback.revision: 33
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 无法推断出变量“&lt;variablename&gt;”的类型，因为它绑定到封闭范围中的某个字段
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

无法推断出变量\<变量名\>的类型，因为它绑定到封闭范围中的某个字段更改\<变量名\>的名称，或者使用完全限定名\(例如，“Me.variablename”或“MyBase.variablename”）。  
  
 您的代码中的循环控制变量的名称与此类的某个字段或其他封闭范围的某个字段的名称相同。  由于此控制变量在使用时未包含 `As` 子句，因此它已绑定到封闭范围中的该字段，并且编译器将不会为该字段创建新的变量或推断其类型。  
  
 在下面的示例中，`For` 语句中的控制变量 `Index` 将绑定到 `Customer` 类中的 `Index` 字段。  编译器不会为控制变量 `Index` 创建新的变量或推断其类型。  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
    ' The following line will raise this warning.  
        For Index = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
  
```  
  
 默认情况下，此消息是一个警告。  有关如何隐藏警告或将警告视为错误的信息，请参见[在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42110  
  
### 处理此警告  
  
-   通过将循环控制变量的名称更改为一个标识符（不是类的字段的名称），使得此变量成为局部变量。  
  
    ```  
    For I = 1 To 10  
    ```  
  
-   阐明如何通过将 `Me.` 作为变量名的前缀，将循环控制变量绑定到类字段。  
  
    ```  
    For Me.Index = 1 To 10  
    ```  
  
-   不依赖于局部类型推断，而是使用 `As` 子句指定循环控制变量的类型。  
  
    ```  
    For Index As Integer = 1 To 10  
    ```  
  
## 示例  
 下面的代码显示已做出初次更正的早期示例。  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
        For I = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
```  
  
## 请参阅  
 [Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [如何：引用对象的当前实例](../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Me、My、MyBase 和 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)