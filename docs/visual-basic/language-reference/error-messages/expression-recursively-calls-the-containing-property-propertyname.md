---
title: "表达式递归调用包含属性“&lt;属性名&gt;” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc42026"
  - "BC42026"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42026"
ms.assetid: 4fde9db6-3bf3-48dc-8e05-981bf08969da
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 表达式递归调用包含属性“&lt;属性名&gt;”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

属性定义的 `Set` 过程中的语句将值存储到属性的名称中。  
  
 保留属性值的建议方法是：在属性的容器中定义一个 `Private` 变量，并将其同时用在 `Get` 和 `Set` 过程中。  `Set` 过程随后应将传入值存储在此 `Private` 变量中。  
  
 `Get` 过程的工作方式类似于 `Function` 过程，因此，当遇到 `End Get` 语句时，它将能够为属性名称赋值并返回控制。  但是，建议的方法是包括 `Private` 变量作为 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 中的值。  
  
 `Set` 过程的工作方式类似于不返回值的 `Sub` 过程。  因此，过程或属性名称在 `Set` 过程中没有特殊含义，并且您无法将值存储到其中。  
  
 下面的示例阐释了可能导致此错误的方法，后面是建议的方法。  
  
```  
Public Class illustrateProperties  
' The code in the following property causes this error.  
    Public Property badProp() As Char  
        Get  
            Dim charValue As Char  
            ' Insert code to update charValue.  
            badProp = charValue  
        End Get  
        Set(ByVal Value As Char)  
            ' The following statement causes this error.  
            badProp = Value  
            ' The value stored in the local variable badProp  
            ' is not used by the Get procedure in this property.  
        End Set  
    End Property  
' The following code uses the recommended approach.  
    Private propValue As Char  
    Public Property goodProp() As Char  
        Get  
            ' Insert code to update propValue.  
            Return propValue  
        End Get  
        Set(ByVal Value As Char)  
            propValue = Value  
        End Set  
    End Property  
End Class  
```  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的更多信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC42026  
  
### 更正此错误  
  
-   重写属性定义，以便使用前面的示例中阐释的建议方法。  
  
## 请参阅  
 [Property 过程](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)