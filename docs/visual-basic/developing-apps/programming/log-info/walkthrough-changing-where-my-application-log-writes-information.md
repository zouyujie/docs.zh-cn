---
title: "演练：更改 My.Application.Log 写入信息的位置 (Visual Basic) | Microsoft Docs"
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
  - "My.Application.Log 对象, 演练"
  - "事件日志, 更改输出位置"
ms.assetid: ecc74f95-743c-450d-93f6-09a30db0fe4a
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 演练：更改 My.Application.Log 写入信息的位置 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以使用 `My.Application.Log` 和 `My.Log` 对象来记录有关应用程序中所发生事件的信息。 本演练将演示如何重写默认设置，以及如何使 `Log` 对象将信息写入其他日志侦听器。  
  
## 系统必备  
 `Log` 对象可以将信息写入多个日志侦听器。 在更改配置之前，需要确定日志侦听器的当前配置。 有关详细信息，请参阅[演练：确定 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)。  
  
 可能需要查看[如何：将事件信息写入文本文件](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)或[如何：写入应用程序事件日志](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)。  
  
### 添加侦听器  
  
1.  在“解决方案资源管理器”中右键单击 app.config，然后选择“打开”。  
  
     \- 或 \-  
  
     如果其中没有 app.config 文件：  
  
    1.  在**“项目”**菜单上选择**“添加新项”**。  
  
    2.  在“添加新项”对话框中，选择“应用程序配置文件”。  
  
    3.  单击**“添加”**。  
  
2.  找到 `<listeners>` 部分，该部分位于 `name` 属性为“DefaultSource”的 `<source>` 部分当中，后者又位于 `<sources>` 部分之下。`<sources>` 部分位于 `<system.diagnostics>` 部分当中，后者又位于顶级 `<configuration>` 部分之下。  
  
3.  将这些元素添加到该 `<listeners>` 部分。  
  
    ```  
    <!-- Uncomment to connect the application file log. -->  
    <!-- <add name="FileLog" /> -->  
    <!-- Uncomment to connect the event log. -->  
    <!-- <add name="EventLog" /> -->  
    <!-- Uncomment to connect the event log. -->  
    <!-- <add name="Delimited" /> -->  
    <!-- Uncomment to connect the XML log. -->  
    <!-- <add name="XmlWriter" /> -->  
    <!-- Uncomment to connect the console log. -->  
    <!-- <add name="Console" /> -->  
    ```  
  
4.  取消注释希望接收 `Log` 消息的日志侦听器。  
  
5.  找到 `<sharedListeners>` 部分，该部分位于 `<system.diagnostics>` 部分当中，后者又位于顶级 `<configuration>` 部分之下。  
  
6.  将这些元素添加到该 `<sharedListeners>` 部分。  
  
    ```  
    <add name="FileLog"  
         type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
               Microsoft.VisualBasic, Version=8.0.0.0,   
               Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"  
         initializeData="FileLogWriter" />  
    <add name="EventLog"  
         type="System.Diagnostics.EventLogTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="sample application"/>  
    <add name="Delimited"   
         type="System.Diagnostics.DelimitedListTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="c:\temp\sampleDelimitedFile.txt"  
         traceOutputOptions="DateTime" />  
    <add name="XmlWriter"  
         type="System.Diagnostics.XmlWriterTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="c:\temp\sampleLogFile.xml" />  
    <add name="Console"  
         type="System.Diagnostics.ConsoleTraceListener,   
               System, Version=2.0.0.0,   
               Culture=neutral, PublicKeyToken=b77a5c561934e089"  
         initializeData="true" />  
    ```  
  
7.  app.config 文件的内容应类似于下面的 XML：  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
              <!-- Uncomment to connect the application file log. -->  
              <!-- <add name="FileLog" /> -->  
              <!-- Uncomment to connect the event log. -->  
              <!-- <add name="EventLog" /> -->  
              <!-- Uncomment to connect the event log. -->  
              <!-- <add name="Delimited" /> -->  
              <!-- Uncomment to connect the XML log. -->  
              <!-- <add name="XmlWriter" /> -->  
              <!-- Uncomment to connect the console log. -->  
              <!-- <add name="Console" /> -->  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="Information" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"  
               initializeData="FileLogWriter" />  
          <add name="EventLog"  
               type="System.Diagnostics.EventLogTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="sample application"/>  
          <add name="Delimited"   
               type="System.Diagnostics.DelimitedListTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="c:\temp\sampleDelimitedFile.txt"  
               traceOutputOptions="DateTime" />  
          <add name="XmlWriter"  
               type="System.Diagnostics.XmlWriterTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="c:\temp\sampleLogFile.xml" />  
          <add name="Console"  
               type="System.Diagnostics.ConsoleTraceListener,   
                     System, Version=2.0.0.0,   
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"  
               initializeData="true" />  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
### 重新配置侦听器  
  
1.  在 `<sharedListeners>` 部分找到侦听器的 `<add>` 元素。  
  
2.  `type` 特性提供了侦听器类型的名称。 此类型必须继承自 <xref:System.Diagnostics.TraceListener> 类。 请使用强名称类型名称以确保使用正确的类型。 有关详细信息，请参阅下面的“引用强名称类型”部分。  
  
     可以使用的类型有：  
  
    -   <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName> 侦听器，它将信息写入文件日志。  
  
    -   <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName> 侦听器，它将信息写入 `initializeData` 参数指定的计算机事件日志。  
  
    -   <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName> 和 <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName> 侦听器，它们将信息写入 `initializeData` 参数指定的文件。  
  
    -   <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName> 侦听器，它将信息写入命令行控制台。  
  
     有关其他类型的日志侦听器写入信息的位置的信息，请参阅该类型的文档。  
  
3.  当应用程序创建日志侦听器对象时，它将传递 `initializeData` 特性作为构造函数参数。`initializeData` 特性的含义取决于跟踪侦听器。  
  
4.  创建日志侦听器后，应用程序将设置该侦听器的属性。 这些属性由 `<add>` 元素中的其他特性定义。 有关特定侦听器的属性的详细信息，请参阅该侦听器类型的文档。  
  
### 引用强名称类型  
  
1.  为确保日志侦听器使用正确的类型，请确保使用完全限定的类型名称和强名称程序集名称。 强名称类型的语法如下所示：  
  
     \<*type name*\>, \<*assembly name*\>, \<*version number*\>, \<*culture*\>, \<*strong name*\>  
  
2.  本代码示例将演示如何在这种情况下确定完全限定类型“System.Diagnostics.FileLogTraceListener”的强命名类型。  
  
     [!code-vb[VbVbalrMyApplicationLog#15](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/visualbasic/VbVbalrMyApplicationLog/Form1.vb#15)]  
  
     它是输出类型，并且可用于唯一引用强名称类型，如上面的“添加侦听器”过程所示。  
  
     `Microsoft.VisualBasic.Logging.FileLogTraceListener, Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a`  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName>   
 <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>   
 [如何：将事件信息写入文本文件](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)   
 [如何：写入应用程序事件日志](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)