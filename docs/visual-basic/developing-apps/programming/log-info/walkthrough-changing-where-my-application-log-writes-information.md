---
title: "更改 My.Application.Log 写入信息的位置 (Visual Basic) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My.Application.Log object, walkthroughs
- event logs, changing output location
ms.assetid: ecc74f95-743c-450d-93f6-09a30db0fe4a
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5e3d68e6a64ec9f8e9cd8bfd13fa8174da568299
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-changing-where-myapplicationlog-writes-information-visual-basic"></a>演练：更改 My.Application.Log 写入信息的位置 (Visual Basic)
可以使用 `My.Application.Log` 和 `My.Log` 对象来记录有关应用程序中所发生事件的信息。 本演练将演示如何重写默认设置，以及如何使 `Log` 对象将信息写入其他日志侦听器。  
  
## <a name="prerequisites"></a>先决条件  
 `Log` 对象可以将信息写入多个日志侦听器。 在更改配置之前，需要确定日志侦听器的当前配置。 有关详细信息，请参阅[演练：确定 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)。  
  
 建议查看[如何：将事件信息写入文本文件](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)或[如何：写入应用程序事件日志](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)。  
  
### <a name="to-add-listeners"></a>添加侦听器  
  
1.  在“解决方案资源管理器” **** 中右键单击 app.config，然后选择“打开” ****。  
  
     \- 或 -  
  
     如果其中没有 app.config 文件：  
  
    1.  在 **“项目”** 菜单上选择 **“添加新项”**。  
  
    2.  在“添加新项” **** 对话框中，选择“应用程序配置文件” ****。  
  
    3.  单击 **“添加”**。  
  
2.  找到 `<listeners>` 部分，该部分位于 `<source>` 属性为“DefaultSource”的 `name` 部分当中，后者又位于 `<sources>` 部分之下。 `<sources>` 部分位于 `<system.diagnostics>` 部分当中，后者又位于顶级 `<configuration>` 部分之下。  
  
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
  
### <a name="to-reconfigure-a-listener"></a>重新配置侦听器  
  
1.  在 `<add>` 部分找到侦听器的 `<sharedListeners>` 元素。  
  
2.  `type` 特性提供了侦听器类型的名称。 此类型必须从 <xref:System.Diagnostics.TraceListener> 类继承。 请使用强名称类型名称以确保使用正确的类型。 有关详细信息，请参阅下面的“引用强名称类型”部分。  
  
     可以使用的类型有：  
  
    -   <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName> 侦听器，用于写入文件日志。  
  
    -   <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName> 侦听器，用于将信息写入 `initializeData` 参数所指定的计算机事件日志。  
  
    -   <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName> 和 <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName> 侦听器，用于写入 `initializeData` 参数中指定的文件。  
  
    -   <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName> 侦听器，用于写入命令行控制台。  
  
     有关其他类型的日志侦听器写入信息的位置的信息，请参阅该类型的文档。  
  
3.  当应用程序创建日志侦听器对象时，它将传递 `initializeData` 特性作为构造函数参数。 `initializeData` 特性的含义取决于跟踪侦听器。  
  
4.  创建日志侦听器后，应用程序将设置该侦听器的属性。 这些属性由 `<add>` 元素中的其他特性定义。 有关特定侦听器的属性的详细信息，请参阅该侦听器类型的文档。  
  
### <a name="to-reference-a-strongly-named-type"></a>引用强名称类型  
  
1.  为确保日志侦听器使用正确的类型，请确保使用完全限定的类型名称和强名称程序集名称。 强名称类型的语法如下所示：  
  
     \<*type name*>, \<*assembly name*>, \<*version number*>, \<*culture*>, \<*strong name*>  
  
2.  本代码示例将演示如何在这种情况下确定完全限定类型“System.Diagnostics.FileLogTraceListener”的强命名类型。  
  
     [!code-vb[VbVbalrMyApplicationLog#15](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-changing-where-my-application-log-writes-information_1.vb)]  
  
     它是输出类型，并且可用于唯一引用强名称类型，如上面的“添加侦听器”过程所示。  
  
     `Microsoft.VisualBasic.Logging.FileLogTraceListener, Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a`  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName>   
 <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>   
 [如何：将事件信息写入文本文件](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)   
 [如何：写入应用程序事件日志](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)
