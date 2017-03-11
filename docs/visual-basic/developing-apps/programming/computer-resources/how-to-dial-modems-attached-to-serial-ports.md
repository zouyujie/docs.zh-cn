---
title: "如何：在 Visual Basic 中使用连接到串行端口的调制解调器拨号 | Microsoft Docs"
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
  - "调制解调器, 拨号"
  - "My.Computer.Ports 对象"
  - "串行端口, 拨号"
ms.assetid: 3834db40-f431-45f1-b671-dc91787164b6
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：在 Visual Basic 中使用连接到串行端口的调制解调器拨号
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本主题介绍如何使用 `My.Computer.Ports` 拨号在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]的调制解调器。  
  
 通常，调制解调器连接到某个计算机的串行端口。  对于您的应用程序与调制解调器进行通信，必须将命令发送到相应的串行端口。  
  
### 使用调制解调器拨号  
  
1.  确定哪个串行端口的调制解调器连接。  此示例假定调制解调器在 COM1。  
  
2.  使用 `My.Computer.Ports.OpenSerialPort` 方法获取对端口。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>。  
  
     `Using` 块允许应用程序关闭串行端口，即使在生成异常。  操作串行端口应出现在块内出现的所有代码，或者在 `Try...Catch...Finally` 块中。  
  
     [!code-vb[VbVbalrMyComputer#28](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/VbVbalrMyComputer/Class2.vb#28)]  
  
3.  设置 `DtrEnable` 属性指示计算机已准备好接受从调制解调器传入的传输。  
  
     [!code-vb[VbVbalrMyComputer#29](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/VbVbalrMyComputer/Class2.vb#29)]  
  
4.  发送拨号命令和电话号码到调制解调器通过串行端口通过 <xref:System.IO.Ports.SerialPort.Write%2A> 方法。  
  
     [!code-vb[VbVbalrMyComputer#30](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/VbVbalrMyComputer/Class2.vb#30)]  
  
## 示例  
 [!code-vb[VbVbalrMyComputer#27](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/VbVbalrMyComputer/Class2.vb#27)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **连接和网络**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
## 编译代码  
 此示例需要引用 <xref:System?displayProperty=fullName> 命名空间。  
  
## 可靠编程  
 此示例假定调制解调器连接到 COM1。  建议您的代码允许用户选择需要的串行端口从可用端口列表。  有关更多信息，请参见 [如何：显示可用的串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)。  
  
 此示例使用 `Using` 块，确保应用程序关闭端口，即使它引发异常。  有关更多信息，请参见 [Using 语句](../../../../visual-basic/language-reference/statements/using-statement.md)。  
  
 在此示例中，，在使用调制解调器拨号之后，应用程序断开串行端口。  实际上，您希望向\/从调制解调器传输数据。  有关更多信息，请参见 [如何：从串行端口接收字符串](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 <xref:System.IO.Ports.SerialPort?displayProperty=fullName>   
 [如何：将字符串发送到串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [如何：从串行端口接收字符串](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-receive-strings-from-serial-ports.md)   
 [如何：显示可用的串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)