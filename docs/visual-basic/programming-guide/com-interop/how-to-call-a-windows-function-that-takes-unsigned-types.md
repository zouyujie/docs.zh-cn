---
title: "如何：调用采用无符号类型的 Windows 函数 (Visual Basic) | Microsoft Docs"
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
  - "数据类型 [Visual Basic], 数值"
  - "数据类型 [Visual Basic], 无符号"
  - "数据类型 [Visual Basic], using"
  - "函数 [Visual Basic], 调用 Windows 函数"
  - "UInteger 数据类型, using"
  - "Ulong 数据类型, using"
  - "无符号数据类型"
  - "无符号类型"
  - "无符号类型, using"
  - "UShort 数据类型, using"
  - "Windows 函数, 调用"
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 如何：调用采用无符号类型的 Windows 函数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

如果您使用类，模块或具有无符号整数的成员的结构类型，则可以访问具有 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]的这些成员。  
  
### 调用采用无符号类型的 windows 函数  
  
1.  使用来 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md) 调用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 哪库包含该函数，确定其名称在库中，确定其调用序列以及将字符串，调用时。  
  
2.  在 `Declare` 语句，请使用 `UInteger`、 `ULong`、 `UShort`或 `Byte` 以适合使用无符号类型的每个参数。  
  
3.  参考要调用的常数的名称和值它使用的 windows 函数的文档。  其中的许多在 WinUser.h 文件中定义的。  
  
4.  在代码中声明必要的常数。  许多 windows 常数是 32 位无符号值，因此，您应声明这些 `As``UInteger`。  
  
5.  以常规方法调用函数。  下面的示例调用 windows 函数 `MessageBox`，采用无符号整数参数。  
  
    ```  
    Public Class windowsMessage  
        Private Declare Auto Function mb Lib "user32.dll" Alias "MessageBox" (  
            ByVal hWnd As Integer,   
            ByVal lpText As String,   
            ByVal lpCaption As String,   
            ByVal uType As UInteger) As Integer  
        Private Const MB_OK As UInteger = 0  
        Private Const MB_ICONEXCLAMATION As UInteger = &H30  
        Private Const IDOK As UInteger = 1  
        Private Const IDCLOSE As UInteger = 8  
        Private Const c As UInteger = MB_OK Or MB_ICONEXCLAMATION  
        Public Function messageThroughWindows() As String  
            Dim r As Integer = mb(0, "Click OK if you see this!",   
                "Windows API call", c)  
            Dim s As String = "Windows API MessageBox returned " &  
                 CStr(r)& vbCrLf & "(IDOK = " & CStr(IDOK) &  
                 ", IDCLOSE = " & CStr(IDCLOSE) & ")"  
            Return s  
        End Function  
    End Class  
    ```  
  
     您可以使用以下代码测试函数 `messageThroughWindows` 。  
  
    ```  
    Public Sub consumeWindowsMessage()  
        Dim w As New windowsMessage  
        w.messageThroughWindows()  
    End Sub  
    ```  
  
    > [!CAUTION]
    >  `UInteger`、 `ULong`、 `UShort`和 `SByte` 数据类型不是 \(cls\) 的 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) 一部分，因此，符合 CLS 的代码不能使用使用其组件。  
  
    > [!IMPORTANT]
    >  调用非托管代码，例如 windows 应用程序编程接口 \(API\) \(api\)，您的代码会有潜在的安全风险。  
  
    > [!IMPORTANT]
    >  调用 windows API 需要非托管代码权限，这可能会影响其在部分信任的情况下执行。  有关更多信息，请参见 <xref:System.Security.Permissions.SecurityPermission> 和 [Code Access Permissions](http://msdn.microsoft.com/zh-cn/e5ae402f-6dda-4732-bbe8-77296630f675)。  
  
## 请参阅  
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)