---
title: "记录来自应用程序的信息 (Visual Basic) | Microsoft Docs"
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
  - "应用程序 [Visual Basic], 记录信息"
  - "示例 [Visual Basic], 记录应用程序信息"
  - "Log 对象"
  - "日志记录"
  - "My.Application.Log 对象"
  - "My.Log 对象"
ms.assetid: 8bf4f047-22d6-48d6-aec5-93b98ad5b8e8
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 记录来自应用程序的信息 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本节包含的主题说明如何使用 `My.Application.Log` 或 `My.Log` 对象记录来自应用程序的信息，以及如何扩展应用程序的日志记录功能。  
  
 `Log` 对象提供了用于将信息写入应用程序的日志侦听器的方法，而 `Log` 对象的高级 `TraceSource` 属性提供了详细的配置信息。  `Log` 对象是由应用程序的配置文件配置的。  
  
 `My.Log` 对象仅可用于 ASP.NET 应用程序。  对于客户端应用程序，请使用 `My.Application.Log`。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.Logging.Log>。  
  
## 任务  
  
|若要|请参见|  
|--------|---------|  
|将事件信息写入应用程序日志。|[如何：编写日志消息](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)|  
|将异常信息写入应用程序日志。|[如何：日志异常](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)|  
|在应用程序启动和关闭时，将跟踪信息写入应用程序的日志中。|[如何：当应用程序启动或关闭时记录消息](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-messages-when-the-application-starts-or-shuts-down.md)|  
|配置 `My.Application.Log`，将信息写入文本文件中。|[如何：将事件信息写入文本文件](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)|  
|配置 `My.Application.Log`，将信息写入事件日志中。|[如何：写入应用程序事件日志](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)|  
|更改 `My.Application.Log` 写入信息的目标位置。|[演练：更改 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)|  
|确定 `My.Application.Log` 写入信息的目标位置。|[演练：确定 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)|  
|为 `My.Application.Log` 创建自定义日志侦听器。|[演练：创建自定义日志侦听器](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-creating-custom-log-listeners.md)|  
|筛选 `My.Application.Log` 日志的输出。|[演练：筛选 My.Application.Log 输出](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)|  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [疑难解答：日志侦听器](../../../../visual-basic/developing-apps/programming/log-info/troubleshooting-log-listeners.md)