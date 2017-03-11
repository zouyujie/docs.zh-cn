---
title: "如何：在 Visual Basic 中将字符串发送到串行端口 | Microsoft Docs"
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
  - "My.Computer.Ports 对象"
  - "端口, 发送字符串到"
  - "串行端口, 发送字符串到"
  - "字符串 [Visual Basic], 发送到串行端口"
ms.assetid: 6ebf46cd-b2d0-4b2c-9a1f-be177b22ad52
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：在 Visual Basic 中将字符串发送到串行端口
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本主题描述在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中如何使用 `My.Computer.Ports` 将字符串发送到计算机的串行端口。  
  
## 示例  
 此示例将字符串发送到 COM1 串行端口。  您可能需要使用计算机上的其他串行端口。  
  
 使用 `My.Computer.Ports.OpenSerialPort` 方法获取对端口的引用。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>。  
  
 `Using` 块允许应用程序即使在生成异常时也关闭串行端口。  操作串行端口的所有代码都应出现在此块中，或者出现在 `Try...Catch...Finally` 块中。  
  
 <xref:System.IO.Ports.SerialPort.WriteLine%2A> 方法将数据发送到此串行端口。  
  
 [!code-vb[VbVbalrMyComputer#33](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/VbVbalrMyComputer/Class2.vb#33)]  
  
## 编译代码  
  
-   此示例假定计算机正在使用 `COM1`。  
  
## 可靠编程  
 此示例假定计算机正在使用 `COM1`；为了获得更大的灵活性，代码应允许用户从可用端口列表中选择需要的串行端口。  有关更多信息，请参见 [如何：显示可用的串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)。  
  
 此示例使用 `Using` 块来确保应用程序关闭端口，即使在引发异常的情况下也关闭端口。  有关更多信息，请参见 [Using 语句](../../../../visual-basic/language-reference/statements/using-statement.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 <xref:System.IO.Ports.SerialPort?displayProperty=fullName>   
 [如何：使用连接到串行端口的调制解调器拨号](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-dial-modems-attached-to-serial-ports.md)   
 [如何：显示可用的串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)