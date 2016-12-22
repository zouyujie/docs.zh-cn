---
title: "如何：编写日志消息 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
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
  - "My.Application.Log 对象, 写入日志消息"
ms.assetid: 972a3e0c-2996-4623-a7a9-d7ebc4d207f8
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：编写日志消息 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

可以使用 `My.Application.Log` 和 `My.Log` 对象来记录有关应用程序的信息。 本示例将演示如何使用 `My.Application.Log.WriteEntry` 方法来记录跟踪信息。  
  
 若要记录异常信息，请使用 `My.Application.Log.WriteException` 方法；有关如何记录异常信息，请参阅[如何：日志异常](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)。  
  
## 示例  
 本示例将使用 `My.Application.Log.WriteEntry` 方法来写出跟踪信息。  
  
 [!CODE [VbVbalrMyApplicationLog#11](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog#11)]  
  
## .NET Framework 安全性  
 请确保写入日志的数据不包含敏感信息，如用户密码。 有关详细信息，请参阅[使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>   
 [使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [如何：日志异常](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [演练：确定 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)   
 [演练：更改 My.Application.Log 写入信息的位置](../Topic/Walkthrough:%20Changing%20Where%20My.Application.Log%20Writes%20Information%20\(Visual%20Basic\).md)   
 [演练：筛选 My.Application.Log 输出](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)