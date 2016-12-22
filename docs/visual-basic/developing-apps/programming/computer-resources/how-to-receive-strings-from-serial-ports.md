---
title: "如何：在 Visual Basic 中从串行端口接收字符串 | Microsoft Docs"
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
  - "My.Resources 对象"
  - "串行端口, 检索字符串"
  - "字符串 [Visual Basic], 从串行端口检索"
ms.assetid: 8371ce2c-e1c7-476b-a86d-9afc2614b6b7
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中从串行端口接收字符串
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

本主题介绍如何使用 `My.Computer.Ports` 从计算机的串行端口接收字符串 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]的。  
  
### 从串行端口接收字符串  
  
1.  初始化返回字符串。  
  
     [!CODE [VbVbalrMyComputer#38](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#38)]  
  
2.  确定应由哪个串行端口提供字符串。  此示例假定它是 `COM1`。  
  
3.  使用 `My.Computer.Ports.OpenSerialPort` 方法获取对端口。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>。  
  
     `Try...Catch...Finally` 块允许应用程序关闭串行端口，即使在生成异常。  所有操作串行端口的代码都应放在此代码块中。  
  
     [!CODE [VbVbalrMyComputer#39](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#39)]  
  
4.  创建读取文本行一个 `Do` 循环，直到没有其他行不可用。  
  
     [!CODE [VbVbalrMyComputer#40](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#40)]  
  
5.  使用 <xref:System.IO.Ports.SerialPort.ReadLine%2A> 方法读取下一行可用文本从串行端口的。  
  
     [!CODE [VbVbalrMyComputer#41](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#41)]  
  
6.  使用一个 `If` 语句 <xref:System.IO.Ports.SerialPort.ReadLine%2A> 确定方法是否返回 \(表示的 `Nothing` 没有其他文本不可用\)。  如果返回 `Nothing`，请退出 `Do` 循环。  
  
     [!CODE [VbVbalrMyComputer#42](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#42)]  
  
7.  添加 `Else` 块。 `If` 语句处理用例该字符串是否实际读取。  块将串行端口中的字符串追加到返回字符串。  
  
     [!CODE [VbVbalrMyComputer#43](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#43)]  
  
8.  返回字符串。  
  
     [!CODE [VbVbalrMyComputer#44](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#44)]  
  
## 示例  
 [!CODE [VbVbalrMyComputer#37](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyComputer#37)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **连接和网络**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
## 编译代码  
 此示例假定计算机正在使用 `COM1`。  
  
## 可靠编程  
 此示例假定计算机正在使用 `COM1`。  为了获得更大的灵活性，代码应允许用户选择需要的串行端口从可用端口列表。  有关更多信息，请参见 [如何：显示可用的串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)。  
  
 此示例使用 `Try...Catch...Finally` 块来确保应用程序关闭端口，并捕捉任何超时异常。  有关更多信息，请参见 [Try...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 <xref:System.IO.Ports.SerialPort?displayProperty=fullName>   
 [如何：使用连接到串行端口的调制解调器拨号](../Topic/How%20to:%20Dial%20Modems%20Attached%20to%20Serial%20Ports%20in%20Visual%20Basic.md)   
 [如何：将字符串发送到串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-send-strings-to-serial-ports.md)   
 [如何：显示可用的串行端口](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-show-available-serial-ports.md)