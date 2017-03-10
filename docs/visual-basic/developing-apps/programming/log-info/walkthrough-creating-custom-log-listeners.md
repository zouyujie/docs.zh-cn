---
title: "演练：创建自定义日志侦听器 (Visual Basic) | Microsoft Docs"
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
  - "自定义日志侦听器"
  - "My.Application.Log 对象, 自定义日志侦听器"
ms.assetid: 0e019115-4b25-4820-afb1-af8c6e391698
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 演练：创建自定义日志侦听器 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此演练演示了如何创建自定义日志侦听器并将其配置为侦听 `My.Application.Log` 对象的输出。  
  
## 入门  
 日志侦听器必须从 <xref:System.Diagnostics.TraceListener> 类继承。  
  
#### 创建侦听器  
  
-   在您的应用程序中，创建一个从 <xref:System.Diagnostics.TraceListener> 继承的名为 `SimpleListener` 的类。  
  
     [!code-vb[VbVbalrMyApplicationLog#16](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/visualbasic/VbVbalrMyApplicationLog/Form1.vb#16)]  
  
     基类所需的 <xref:System.Diagnostics.TraceListener.Write%2A> 和 <xref:System.Diagnostics.TraceListener.WriteLine%2A> 方法调用 `MsgBox` 以显示其输出。  
  
     <xref:System.Security.Permissions.HostProtectionAttribute> 特性应用于 <xref:System.Diagnostics.TraceListener.Write%2A> 和 <xref:System.Diagnostics.TraceListener.WriteLine%2A> 方法，因此这两个方法的特性匹配基类方法。  通过 <xref:System.Security.Permissions.HostProtectionAttribute> 特性，运行代码的主机可以确定由代码公开主机保护的同步。  
  
    > [!NOTE]
    >  仅在承载公共语言运行时且实现主机保护的非托管应用程序上（如 SQL Server），<xref:System.Security.Permissions.HostProtectionAttribute> 特性才有效。  
  
 为确保 `My.Application.Log` 使用您的日志侦听器，应为包含您的日志侦听器的程序集指定强名称。  
  
 下一个过程提供了创建强名称日志侦听器程序集的一些简单步骤。  有关更多信息，请参见[创建和使用具有强名称的程序集](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md)。  
  
#### 为日志侦听器程序集指定强名称  
  
1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，选择**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击**“签名”**选项卡。  
  
3.  选择**“为程序集签名”**框。  
  
4.  从**“选择强名称密钥文件”**下拉列表中选择**“\<新建\>”**。  
  
     将打开**“创建强名称密钥”**对话框。  
  
5.  在**“密钥文件名称”**框中提供密钥文件的名称。  
  
6.  在**“输入密码”**和**“确认密码”**框中输入一个密码。  
  
7.  单击**“确定”**。  
  
8.  重新生成应用程序。  
  
## 添加侦听器  
 既然程序集已具有强名称，您就需要确定侦听器的强名称，以便 `My.Application.Log` 可以使用您的日志侦听器。  
  
 强名称类型的格式如下所示。  
  
 \<类型名称\>, \<程序集名称\>, \<版本号\>, \<区域性\>, \<强名称\>  
  
#### 确定侦听器的强名称  
  
-   下面的代码演示了如何确定 `SimpleListener` 的强名称类型的名称。  
  
     [!code-vb[VbVbalrMyApplicationLog#17](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/visualbasic/VbVbalrMyApplicationLog/Form1.vb#17)]  
  
     类型的强名称取决于您的项目。  
  
 通过强名称，可以将侦听器添加到 `My.Application.Log` 日志侦听器集合。  
  
#### 将侦听器添加到 My.Application.Log  
  
1.  在**“解决方案资源管理器”**中右击 app.config，然后选择**“打开”**。  
  
     \- 或 \-  
  
     如果存在一个 app.config 文件：  
  
    1.  在**“项目”**菜单上选择**“添加新项”**。  
  
    2.  在**“添加新项”**对话框中，选择**“应用程序配置文件”**。  
  
    3.  单击**“添加”**。  
  
2.  在具有 `name` 特性“DefaultSource”的 `<source>` 节（位于 `<sources>` 节中）中找到 `<listeners>` 节。  `<sources>` 节位于顶级 `<configuration>` 节的 `<system.diagnostics>` 节中。  
  
3.  将此元素添加到 `<listeners>` 节中：  
  
    ```  
    <add name="SimpleLog" />  
    ```  
  
4.  在顶级 `<configuration>` 节的 `<system.diagnostics>` 节中找到 `<sharedListeners>` 节。  
  
5.  将此元素添加到该 `<sharedListeners>` 节中：  
  
    ```  
    <add name="SimpleLog" type="SimpleLogStrongName" />  
    ```  
  
     将 `SimpleLogStrongName` 的值更改为侦听器的强名称。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [使用 Application 日志](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [如何：日志异常](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [如何：编写日志消息](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [演练：更改 My.Application.Log 写入信息的位置](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)