---
title: "使用 Visual Basic 在 .NET Framework 中执行的端口操作 | Microsoft Docs"
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
  - "端口, Visual Basic"
ms.assetid: 1eba223b-7bd3-401a-b097-982bce96df1b
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 使用 Visual Basic 在 .NET Framework 中执行的端口操作
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

您可以通过 <xref:System.IO.Ports?displayProperty=fullName> 命名空间中的 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 类访问您的计算机的串行端口。  最重要的类 <xref:System.IO.Ports.SerialPort> 为同步和事件驱动 I\/O 提供框架，提供对插针和中断状态的访问以及对串行驱动程序属性的访问。  它可以包装在可通过 <xref:System.IO.Ports.SerialPort.BaseStream%2A> 属性访问的 <xref:System.IO.Stream> 对象中。  通过将 <xref:System.IO.Ports.SerialPort> 包装在 <xref:System.IO.Stream> 对象中，可允许使用流的类访问串行端口。  该命名空间包含可以简化对串行端口的控制的枚举。  
  
 创建 <xref:System.IO.Ports.SerialPort> 对象的最简单的方法是通过 <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A> 方法创建。  
  
> [!NOTE]
>  不能使用 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 类直接访问其他类型的端口，如并行端口、USB 端口等。  
  
## 枚举  
 此表列出并描述了用于访问串行端口的主要枚举：  
  
|||  
|-|-|  
|Enumeration|说明|  
|<xref:System.IO.Ports.Handshake>|指定在为 <xref:System.IO.Ports.SerialPort> 对象建立串行端口通信时使用的控制协议。|  
|<xref:System.IO.Ports.Parity>|指定 <xref:System.IO.Ports.SerialPort> 对象的奇偶校验位。|  
|<xref:System.IO.Ports.SerialData>|指定在 <xref:System.IO.Ports.SerialPort> 对象的串行端口上收到的字符的类型。|  
|<xref:System.IO.Ports.SerialError>|指定在 <xref:System.IO.Ports.SerialPort> 对象上发生的错误。|  
|<xref:System.IO.Ports.SerialPinChange>|指定在 <xref:System.IO.Ports.SerialPort> 对象上发生的更改的类型。|  
|<xref:System.IO.Ports.StopBits>|指定在 <xref:System.IO.Ports.SerialPort> 对象上使用的停止位的数目。|  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 [访问计算机的端口](../../../../visual-basic/developing-apps/programming/computer-resources/accessing-the-computer-s-ports.md)