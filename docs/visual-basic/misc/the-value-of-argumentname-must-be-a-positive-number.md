---
title: "&lt;argumentname&gt; 的值必须是正数 | Microsoft Docs"
ms.custom: ""
ms.date: "11/17/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrApplicationLog_NegativeNumber"
ms.assetid: 597c412c-499e-49d2-b656-af2d90c292a5
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;argumentname&gt; 的值必须是正数
<xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.ReserveDiskSpace%2A> 属性的值必须大于零。  
  
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.ReserveDiskSpace%2A> 属性有必要在消息可写入日志文件之前指定可用磁盘空间量（以字节为单位）。  
  
### 更正此错误  
  
-   将 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.ReserveDiskSpace%2A> 属性设置为正数。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.ReserveDiskSpace%2A>   
 [My.Application.Log 对象](../../visual-basic/language-reference/objects/my-application-log-object.md)   
 [My.Log 对象](../../visual-basic/language-reference/objects/my-log-object.md)