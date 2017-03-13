---
title: "疑难解答：日志侦听器 (Visual Basic) | Microsoft Docs"
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
  - "事件日志, 疑难解答"
  - "事件日志疑难解答"
  - "Visual Basic 疑难解答, 事件日志"
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 疑难解答：日志侦听器 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以使用 `My.Application.Log` 和 `My.Log` 对象记录有关应用程序中发生的事件的信息。  
  
 若要确定哪些日志侦听器接收这些消息，请参见 [演练：确定 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)。  
  
 `Log` 对象可以使用日志筛选来限制它所记录的信息量。  如果筛选配置不正确，则日志可能包含错误的信息。  有关筛选的更多信息，请参见 [演练：筛选 My.Application.Log 输出](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)。  
  
 但是，如果日志配置不正确，则可能需要有关其当前配置的更多信息。  可以通过日志的 `TraceSource` 高级属性获取此信息。  
  
### 为代码中的日志对象确定日志侦听器  
  
1.  在代码文件的开头导入 <xref:System.Diagnostics> 命名空间。  有关更多信息，请参见 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
     [!code-vb[VbVbalrMyApplicationLog#13](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_1.vb)]  
  
2.  创建一个函数，用于返回由每个日志侦听器的信息组成的字符串。  
  
     [!code-vb[VbVbalrMyApplicationLog#14](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_2.vb)]  
  
3.  将日志的跟踪侦听器集合传递给 `GetListeners` 函数，并显示返回值。  
  
     [!code-vb[VbVbalrMyApplicationLog#19](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_3.vb)]  
  
     有关更多信息，请参见 <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A>。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [演练：确定 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)