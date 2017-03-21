---
title: "演练：确定 My.Application.Log 写入信息的位置 (Visual Basic) | Microsoft Docs"
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
  - "My.Log 对象, 输出位置"
  - "输出, 应用程序日志位置"
  - "My.Application.Log 对象, 输出位置"
  - "事件日志, 确定输出位置"
  - "应用程序事件日志, 输出位置"
  - "应用程序 [Visual Basic], 输出位置"
ms.assetid: 5b70143a-7741-45f2-ae1d-03324a3a4189
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# 演练：确定 My.Application.Log 写入信息的位置 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`My.Application.Log` 对象可以将信息写入多个日志侦听器。 日志侦听器由计算机的配置文件配置，并且可以通过应用程序的配置文件重写。 本主题介绍默认设置以及如何确定应用程序的设置。  
  
 有关默认输出位置的详细信息，请参阅[使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)。  
  
### 确定 My.Application.Log 的侦听器  
  
1.  找到程序集的配置文件。 如果正在开发程序集，则可以通过“解决方案资源管理器” 访问 [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] 中的 app.config。 否则，配置文件名称即为程序集的名称附加“.config”，并且与程序集位于相同的目录中。  
  
    > [!NOTE]
    >  不是每个程序集都有配置文件。  
  
     配置文件是一个 XML 文件。  
  
2.  找到 `<listeners>` 部分，该部分位于 `name` 属性为“DefaultSource”的 `<source>` 部分当中，后者又位于 `<sources>` 部分之下。`<sources>` 部分位于 `<system.diagnostics>` 部分当中，后者又位于顶级 `<configuration>` 部分之下。  
  
     如果这些部分不存在，则计算机的配置文件可能会配置 `My.Application.Log` 日志侦听器。 以下步骤介绍如何确定计算机配置文件定义的内容：  
  
    1.  找到计算机的 machine.config 文件。 通常情况下，该文件位于 *SystemRoot\\Microsoft.NET\\Framework\\frameworkVersion\\CONFIG* 目录，其中 `SystemRoot` 是操作系统目录，`frameworkVersion` 是 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 的版本。  
  
         machine.config 中的设置可以通过应用程序的配置文件重写。  
  
         如果如下所列的可选元素不存在，可以创建它们。  
  
    2.  找到 `<listeners>` 部分，该部分位于 `name` 属性为“DefaultSource”的 `<source>` 部分当中，后者又位于 `<sources>` 部分当中，这部分位于 `<system.diagnostics>` 部分当中，位于顶级 `<configuration>` 部分之下。  
  
         如果这些部分不存在，则 `My.Application.Log` 将只有默认的日志侦听器。  
  
3.  在 `listeners>` 部分找到 `add>` 元素。  
  
     这些元素会将命名的日志侦听器添加到 `My.Application.Log` 源。  
  
4.  在 `<sharedListeners>` 部分找到具有日志侦听器名称的 `<add>` 元素，该部分位于 `<system.diagnostics>` 部分当中，后者又位于顶级 `<configuration>` 部分之下。  
  
5.  对于许多类型的共享侦听器，该侦听器的初始化数据说明了侦听器写入数据的位置：  
  
    -   <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName> 侦听器将信息写入文件日志，如简介中所述。  
  
    -   <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName> 侦听器将信息写入 `initializeData` 参数指定的计算机事件日志。 若要查看事件日志，可以使用“服务器资源管理器”或“Windows 事件查看器”。 有关详细信息，请参阅[.NET Framework 中的 ETW 事件](../Topic/ETW%20Events%20in%20the%20.NET%20Framework.md)。  
  
    -   <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName> 和 <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName> 侦听器将信息写入 `initializeData` 参数指定的文件。  
  
    -   <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName> 侦听器将信息写入命令行控制台。  
  
    -   有关其他类型的日志侦听器写入信息的位置的信息，请参阅该类型的文档。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:System.Diagnostics.DefaultTraceListener>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 <xref:System.Diagnostics.DelimitedListTraceListener>   
 <xref:System.Diagnostics.XmlWriterTraceListener>   
 <xref:System.Diagnostics.ConsoleTraceListener>   
 <xref:System.Diagnostics>   
 [使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [如何：日志异常](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [如何：编写日志消息](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [演练：更改 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)   
 [.NET Framework 中的 ETW 事件](../Topic/ETW%20Events%20in%20the%20.NET%20Framework.md)   
 [疑难解答：日志侦听器](../../../../visual-basic/developing-apps/programming/log-info/troubleshooting-log-listeners.md)