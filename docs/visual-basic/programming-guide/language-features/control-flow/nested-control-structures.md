---
title: "嵌套的控件结构 (Visual Basic) | Microsoft Docs"
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
helpviewer_keywords: 
  - "条件语句, 嵌套"
  - "控制流, 嵌套的控制语句"
  - "控件结构, 嵌套"
  - "嵌套的控制语句"
  - "语句 [Visual Basic], 控制流"
  - "结构, 嵌套的控件"
  - "Visual Basic 代码, 控制流"
ms.assetid: cf60b061-65d9-44a8-81f2-b0bdccd23a05
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 嵌套的控件结构 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以放置在其他控制语句中的控制语句，如 `If...Then...Else` 在 `For...Next` 循环块中。  控制语句放在另一个控制语句中称为 " *嵌套*。  
  
## 嵌套级别  
 ，当需要，在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 的控制结构可以嵌套到多个级别。  是为了使嵌套结构可读通过缩进每个的主体。  集成 \(IDE\)开发环境 \(ide\) 编辑器自动执行此操作。  
  
 在下面的示例中，过程 `sumRows` 以将矩阵每一行的正元素。  
  
```  
Public Sub sumRows(ByVal a(,) As Double, ByRef r() As Double)  
    Dim i, j As Integer  
    For i = 0 To UBound(a, 1)  
        r(i) = 0  
        For j = 0 To UBound(a, 2)  
            If a(i, j) > 0 Then  
                r(i) = r(i) + a(i, j)  
            End If  
        Next j  
    Next i  
End Sub  
```  
  
 在前面的示例中，第一个 `Next` 语句关闭内部 `For` 周期，并且最后 `Next` 语句关闭外部 `For` 循环。  
  
 同样，在嵌套的 `If` 语句， `End If` 语句自动应用于最近的早期 `If` 语句。  嵌套 `Do` 循环类似地，并与最里层 `Do` 语句的最内层的 `Loop` 语句一起使用。  
  
> [!NOTE]
>  对于许多控制结构，那么，当您单击某个关键字时，结构中的所有关键字都会突出显示。  例如，那么，当您在 `If...Then...Else` 构造中单击时 `If` ， `If`、 `Then`、 `ElseIf`、 `Else`和`End If` 所有实例该构造中显示。  若要移动到下一个或上一个突出显示的关键字，请按 ctrl\+shift\+ 向下键或 ctrl\+shift\+ 向上键。  
  
## 嵌套不同类型的控制结构  
 可以嵌套在另一个类型中的控制结构。  下面的示例使用 `With` 块在 `For Each` 循环内，并且嵌套的 `If` 块在 `With` 块。  
  
```  
For Each ctl As System.Windows.Forms.Control In Me.Controls  
    With ctl  
        .BackColor = System.Drawing.Color.Yellow  
        .ForeColor = System.Drawing.Color.Black  
        If .CanFocus Then  
            .Text = "Colors changed"  
            If Not .Focus() Then  
                ' Insert code to process failed focus.  
            End If  
        End If  
    End With  
Next ctl  
```  
  
## 重叠控制结构  
 不能重叠控制结构。  这意味着必须在下最内层的结构内完全包含所有嵌套结构。  例如，下面的排列是无效的，因为 `For` 停止循环，在内部 `With` 块停止之前。  
  
 ![无效嵌套示意图](../../../../visual-basic/programming-guide/language-features/control-flow/media/nestexampleinvalid.png "NestExampleInvalid")  
无效嵌套和 with 结构的  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器检测到这样的重叠控制结构并发出编译时错误。  
  
## 请参阅  
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [决策结构](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [其他控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)