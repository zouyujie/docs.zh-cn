---
title: "如何：将事件信息写入文本文件 (Visual Basic) | Microsoft Docs"
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
  - "事件日志 [Visual Studio], 写入事件信息"
  - "事件 [Visual Basic], 将事件信息写入文本文件"
  - "文本文件, 将事件信息写入文本文件"
ms.assetid: 9ca7cc03-bf99-4933-9e5e-61ee28e9a6b4
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 如何：将事件信息写入文本文件 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以使用 `My.Application.Log` 和 `My.Log` 对象记录有关应用程序中发生的事件的信息。  此示例演示如何使用 `My.Application.Log.WriteEntry` 方法将跟踪信息记录到日志文件中。  
  
### 添加和配置文件日志侦听器  
  
1.  在**“解决方案资源管理器”**中右击“app.config”，然后选择**“打开”**。  
  
     \- 或 \-  
  
     如果没有 app.config 文件，则：  
  
    1.  在**“项目”**菜单上选择**“添加新项”**。  
  
    2.  在**“添加新项”**对话框中，选择**“应用程序配置文件”**。  
  
    3.  单击**“添加”**。  
  
2.  在应用程序配置文件中找到 `<listeners>` 节。  
  
     可以在 name 特性为“DefaultSource”的 \<source\> 节中找到 \<listeners\> 节，前者嵌套在嵌套于顶级 \<configuration\> 节下的 \<system.diagnostics\> 节中。  
  
3.  将此元素添加到该 `<listeners>` 节中：  
  
    ```  
    <add name="FileLogListener" />  
    ```  
  
4.  在 `<system.diagnostics>` 节（嵌套在顶级 `<configuration>` 节下）中找到 `<sharedListeners>` 节。  
  
5.  将此元素添加到该 `<sharedListeners>` 节中：  
  
    ```  
    <add name="FileLogListener"   
        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
              Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,   
              PublicKeyToken=b03f5f7f11d50a3a"  
        initializeData="FileLogListenerWriter"  
        location="Custom"  
        customlocation="c:\temp\" />  
    ```  
  
     将 `customlocation` 特性的值更改为日志目录。  
  
    > [!NOTE]
    >  若要设置侦听器属性的值，请使用与该属性名称相同并且名称中的所有字母都是小写的特性。  例如，`location` 和 `customlocation` 特性设置 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.Location%2A> 和 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.CustomLocation%2A> 属性的值。  
  
### 将事件信息写入文件日志  
  
-   使用 `My.Application.Log.WriteEntry` 或 `My.Application.Log.WriteException` 方法将信息写入文件日志中。  有关更多信息，请参见 [如何：编写日志消息](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md) 和 [如何：日志异常](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)。  
  
     在为程序集配置文件日志侦听器后，该侦听器即可接收 `My.Application.Log` 从该程序集写入的所有消息。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>   
 <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>   
 [使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [如何：日志异常](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)