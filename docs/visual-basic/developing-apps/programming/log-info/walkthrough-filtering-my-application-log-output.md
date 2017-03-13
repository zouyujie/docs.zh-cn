---
title: "演练：筛选 My.Application.Log 输出 (Visual Basic) | Microsoft Docs"
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
  - "My.Log 对象，筛选输出"
  - "My.Application.Log 对象，筛选输出"
  - "应用程序事件日志输出筛选"
ms.assetid: 2c0a457a-38a4-49e1-934d-a51320b7b4ca
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# 演练：筛选 My.Application.Log 输出 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本演练演示如何更改默认日志筛选 `My.Application.Log` 对象，来控制哪些信息从传递 `Log` 到侦听器由侦听器编写哪些信息的对象。 您可以构建应用程序，即使更改日志记录行为，因为在应用程序的配置文件中存储的配置信息。  
  
## <a name="getting-started"></a>入门  
 每条消息都 `My.Application.Log` 写入操作都有相关的严重程度级别，哪些筛选机制用于控制日志输出。 此示例应用程序使用 `My.Application.Log` 方法来写入多个具有不同严重性级别记录消息。  
  
#### <a name="to-build-the-sample-application"></a>若要生成示例应用程序  
  
1.  打开一个新 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] Windows 应用程序项目。  
  
2.  添加一个名为 form1 为 Button1 的按钮。  
  
3.  在 <xref:System.Windows.Forms.Control.Click> 为 Button1，事件处理程序添加以下代码︰  
  
     [!code-vb[VbVbcnMyApplicationLogFiltering#1](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-filtering-my-application-log-output_1.vb)]  
  
4.  在调试器中运行该应用程序。  
  
5.  按 **Button1**。  
  
     应用程序在应用程序的调试输出和日志文件中写入以下信息。  
  
     `DefaultSource Information: 0 : In Button1_Click`  
  
     `DefaultSource Error: 2 : Error in the application.`  
  
6.  关闭该应用程序。  
  
     有关如何查看应用程序的调试输出窗口的信息，请参阅 [输出窗口](/visual-studio/ide/reference/output-window)。 应用程序的日志文件的位置的信息，请参阅 [演练︰ 确定其中 My.Application.Log 写入信息](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)。  
  
    > [!NOTE]
    >  默认情况下，应用程序关闭时刷新日志文件的输出。  
  
     在上例中，第二次调用 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A> 方法，并对调用 <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A> 方法产生日志输出，同时对的第一个和最后一个调用 `WriteEntry` 方法不这样做。 这是因为的严重级别 `WriteEntry` 和 `WriteException` 为"信息"和"错误"，这两种所允许的 `My.Application.Log` 对象的默认日志筛选。 但是，对于"开始"和"Stop"严重级别的事件将不能产生日志输出。  
  
## <a name="filtering-for-all-myapplicationlog-listeners"></a>对所有 My.Application.Log 侦听器的筛选  
  `My.Application.Log` 对象使用 <xref:System.Diagnostics.SourceSwitch> 名为 `DefaultSwitch` 以控制哪些从传递的消息 `WriteEntry` 和 `WriteException` 写入日志侦听器方法。 您可以配置 `DefaultSwitch` 通过将其值设置为其中一个应用程序的配置文件中 <xref:System.Diagnostics.SourceLevels> 枚举值。 默认情况下，其值为"信息"。  
  
 此表显示了所需的日志，以将消息写入到侦听器，给定特定严重性级别 `DefaultSwitch` 设置。  
  
|||  
|-|-|  
|DefaultSwitch 值|所需的输出的消息严重性|  
|`Critical`|`Critical`|  
|`Error`|`Critical` 或 `Error`|  
|`Warning`|`Critical`、`Error` 或 `Warning`|  
|`Information`|`Critical`、`Error`、`Warning` 或 `Information`|  
|`Verbose`|`Critical`、`Error`、`Warning`、`Information` 或 `Verbose`|  
|`ActivityTracing`|`Start`、`Stop`、`Suspend`、`Resume` 或 `Transfer`|  
|`All`|允许所有的消息。|  
|`Off`|阻止所有的消息。|  
  
> [!NOTE]
>   `WriteEntry` 和 `WriteException` 方法都有一个重载，未指定严重级别。 隐式的严重性级别 `WriteEntry` 重载是"信息"且的隐式的严重性级别 `WriteException` 重载是"错误"。  
  
 下表介绍在前面的示例所示的日志输出︰ 使用默认 `DefaultSwitch` 设置为"信息"，仅第二次调用到 `WriteEntry` 方法，并对调用 `WriteException` 方法生成的日志输出。  
  
#### <a name="to-log-only-activity-tracing-events"></a>记录活动才跟踪事件  
  
1.  用鼠标右键单击 app.config 中的 **解决方案资源管理器** ，然后选择 **打开**。  
  
     - 或 -  
  
     如果其中没有 app.config 文件：  
  
    1.  在 **“项目”** 菜单上选择 **“添加新项”**。  
  
    2.  在“添加新项”  对话框中，选择“应用程序配置文件” 。  
  
    3.  单击 **“添加”**。  
  
2.  找到 `<switches>` 部分中，该对话框位于 `<system.diagnostics>` 部分中，这是在顶级 `<configuration>` 部分。  
  
3.  找到将添加的元素 `DefaultSwitch` 到交换机的集合。 其外观应类似于此元素︰  
  
     `<add name="DefaultSwitch" value="Information" />`  
  
4.  值更改 `value` 属性设为"ActivityTracing"。  
  
5.  app.config 文件的内容应类似于下面的 XML：  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="ActivityTracing" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
6.  在调试器中运行该应用程序。  
  
7.  按 **Button1**。  
  
     应用程序在应用程序的调试输出和日志文件中写入以下信息︰  
  
     `DefaultSource Start: 4 : Entering Button1_Click`  
  
     `DefaultSource Stop: 5 : Leaving Button1_Click`  
  
8.  关闭该应用程序。  
  
9. 值更改 `value` 回"信息"属性。  
  
    > [!NOTE]
    >   `DefaultSwitch` 开关设置仅控制 `My.Application.Log`。 它不会更改如何 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] <xref:System.Diagnostics.Trace?displayProperty=fullName> 和 <xref:System.Diagnostics.Debug?displayProperty=fullName> 类的行为。  
  
## <a name="individual-filtering-for-myapplicationlog-listeners"></a>单个筛选 My.Application.Log 侦听器  
 上面的示例演示如何更改所有筛选 `My.Application.Log` 输出。 此示例演示如何进行筛选的单独的日志侦听器。 默认情况下，应用程序有两个侦听器，用于写入应用程序的调试输出和日志文件。  
  
 配置文件控制的日志侦听器行为通过允许每个拥有一个筛选器，这类似于开关 `My.Application.Log`。 日志侦听器将输出一条消息，仅当消息的严重性允许由这两个日志的 `DefaultSwitch` 和日志侦听器的筛选器。  
  
 此示例演示如何为新的调试侦听器配置筛选并将其添加到 `Log` 对象。 应从删除默认的调试侦听器 `Log` 对象，因此很显然调试消息来自新的调试侦听器。  
  
#### <a name="to-log-only-activity-tracing-events"></a>仅要记录的活动跟踪事件  
  
1.  用鼠标右键单击 app.config 中的 **解决方案资源管理器** ，然后选择 **打开**。  
  
     - 或 -  
  
     如果其中没有 app.config 文件：  
  
    1.  在 **“项目”** 菜单上选择 **“添加新项”**。  
  
    2.  在“添加新项”  对话框中，选择“应用程序配置文件” 。  
  
    3.  单击 **“添加”**。  
  
2.  用鼠标右键单击 app.config 中的 **解决方案资源管理器**。 选择 **打开**。  
  
3.  找到 `<listeners>` 部分中，在 `<source>` 部分与 `name` 特性"DefaultSource"，低于 `<sources>` 部分。  `<sources>` 节位于 `<system.diagnostics>` 部分中的，在顶级 `<configuration>` 部分。  
  
4.  此将元素添加到 `<listeners>` 部分︰  
  
    ```xml  
    <!-- Remove the default debug listener. -->  
    <remove name="Default"/>  
    <!-- Add a filterable debug listener. -->  
    <add name="NewDefault"/>  
    ```  
  
5.  找到 `<sharedListeners>` 部分，该部分位于 `<system.diagnostics>` 部分当中，后者又位于顶级 `<configuration>` 部分之下。  
  
6.  将此元素添加到该 `<sharedListeners>` 部分：  
  
    ```xml  
    <add name="NewDefault"   
         type="System.Diagnostics.DefaultTraceListener,   
               System, Version=2.0.0.0, Culture=neutral,   
               PublicKeyToken=b77a5c561934e089,   
               processorArchitecture=MSIL">  
        <filter type="System.Diagnostics.EventTypeFilter"   
                initializeData="Error" />  
    </add>  
    ```  
  
      <xref:System.Diagnostics.EventTypeFilter> 筛选器将其中的一个 <xref:System.Diagnostics.SourceLevels> 枚举值，则为其 `initializeData` 属性。  
  
7.  app.config 文件的内容应类似于下面的 XML：  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
              <!-- Remove the default debug listener. -->  
              <remove name="Default"/>  
              <!-- Add a filterable debug listener. -->  
              <add name="NewDefault"/>  
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
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
          <add name="NewDefault"   
               type="System.Diagnostics.DefaultTraceListener,   
                     System, Version=2.0.0.0, Culture=neutral,   
                     PublicKeyToken=b77a5c561934e089,   
                     processorArchitecture=MSIL">  
            <filter type="System.Diagnostics.EventTypeFilter"   
                    initializeData="Error" />  
          </add>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
8.  在调试器中运行该应用程序。  
  
9. 按 **Button1**。  
  
     应用程序在应用程序的日志文件中写入以下信息︰  
  
     `Default Information: 0 : In Button1_Click`  
  
     `Default Error: 2 : Error in the application.`  
  
     应用程序由于限制性更强的筛选将较少的信息写入到应用程序的调试输出。  
  
     `Default Error   2   Error`  
  
10. 关闭该应用程序。  
  
 有关在部署后更改日志设置的详细信息，请参阅 [使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [演练︰ 确定 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)   
 [演练︰ 更改 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)   
 [演练︰ 创建自定义日志侦听器](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-creating-custom-log-listeners.md)   
 [如何︰ 编写日志消息](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [跟踪开关](../Topic/Trace%20Switches.md)   
 [记录来自应用程序的信息](../../../../visual-basic/developing-apps/programming/log-info/logging-information-from-the-application.md)