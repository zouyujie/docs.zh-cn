---
title: "如何：启动应用程序并向其发送击键 (Visual Basic) | Microsoft Docs"
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
  - "击键, 发送"
  - "进程, 启动和发送击键"
  - "SendKeys.SendWait 示例"
  - "Shell 命令示例 [Visual Basic]"
ms.assetid: f1303184-fce4-44fb-88b4-aac5f42d5d77
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：启动应用程序并向其发送击键 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例使用 `Shell` 函数启动计算器应用程序然后使用两个数字以发送键击使用 `My.Computer.Keyboard.SendKeys` 方法。  
  
## 示例  
 [!code-vb[VbVbalrMyComputer#25](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/VbVbalrMyComputer/Class2.vb#25)]  
  
## 可靠编程  
 ，当与请求的应用程序进程标识符无法找到， <xref:System.ArgumentException> 将引发异常。  
  
## .NET Framework 安全性  
 为 `Shell` 函数的调用要求完全信任 \(<xref:System.Security.SecurityException> 类\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Keyboard.SendKeys%2A>   
 <xref:Microsoft.VisualBasic.Interaction.Shell%2A>   
 <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>