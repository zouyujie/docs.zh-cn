---
title: "如何：在 Visual Basic 中显示可用的串行端口 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Computer.Ports 对象"
  - "My.Computer.Ports.SerialPortNames 属性"
  - "端口, 串行端口可用性"
  - "串行端口, 可用性"
ms.assetid: eaf2ee5a-8103-4e10-a205-ed1d4db120ba
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中显示可用的串行端口
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

本主题介绍 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]描述如何使用 `My.Computer.Ports` 显示计算机的可用串行端口。  
  
 允许用户选择要使用的端口，串行端口的名称。 <xref:System.Windows.Forms.ListBox> 控件放在。  
  
## 示例  
 此示例循环访问 `My.Computer.Ports.SerialPortNames` 属性返回的字符串。  这些字符串是可用串行端口的名称在计算机上。  
  
 通常，串行端口应用程序应从可用端口列表中使用的用户选择。  在本示例中，串行端口的名称在 <xref:System.Windows.Forms.ListBox> 控件存储。  有关更多信息，请参见 [ListBox 控件](../Topic/ListBox%20Control%20\(Windows%20Forms\).md)。  
  
 [!CODE [VbVbalrMyComputer#45](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#45)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **连接和网络**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
## 编译代码  
 此示例需要:  
  
-   项目对 System.Windows.Forms.dll。  
  
-   为 <xref:System.Windows.Forms> 命名空间的成员。  没有完全限定，则需要在代码中，的成员名称添加一个 `Imports` 语句。  有关更多信息，请参见 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
-   窗体上有一个 <xref:System.Windows.Forms.ListBox> 名为的控件 `ListBox1`。  
  
## 可靠编程  
 您不必使用 <xref:System.Windows.Forms.ListBox> 控件显示可用串行端口的名称。  相反，可以使用 <xref:System.Windows.Forms.ComboBox> 或其他控件。  如果应用程序不需要来自用户的响应，可以使用 <xref:System.Windows.Forms.TextBox> 控件显示信息。  
  
> [!NOTE]
>  `My.Computer.Ports.SerialPortNames` 返回的端口名称在 Windows 98 可能不正确，当运行。  ，在使用端口名打开端口时，为了防止应用程序错误，请使用异常处理，例如 `Try...Catch...Finally` 语句或 `Using` 语句。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 [如何：使用连接到串行端口的调制解调器拨号](../Topic/How%20to:%20Dial%20Modems%20Attached%20to%20Serial%20Ports%20in%20Visual%20Basic.md)   
 [如何：将字符串发送到串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [如何：从串行端口接收字符串](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)