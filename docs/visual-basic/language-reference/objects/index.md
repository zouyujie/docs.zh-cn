---
title: "对象 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "对象 [Visual Basic]"
ms.assetid: 651c73e4-dca8-402b-9c6b-e3902b3a3f4b
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 对象 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本主题提供指向其他主题的链接，这些主题记录 Visual Basic 运行时对象并包含其成员过程、属性、和事件的表。  
  
## Visual Basic 运行时对象  
  
|||  
|-|-|  
|<xref:Microsoft.VisualBasic.Collection>|提供一种将一组相关项视为单个对象的便捷方法。|  
|<xref:Microsoft.VisualBasic.Information.Err%2A>|包含有关运行时错误的信息。|  
|`My.Application` 对象由以下类组成：<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase> 提供在所有项目中可用的成员。<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 提供在 Windows 窗体应用程序中可用的成员。<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> 提供在控制台应用程序中可用的成员。|提供仅与当前应用程序或 DLL 关联的数据。  无法利用 `My.Application` 更改任何系统级别的信息。<br /><br /> 某些成员仅对 Windows 窗体或控制台应用程序可用。|  
|`My.Application.Info` \(<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Info%2A>\)|提供用于获取有关应用程序的信息（例如版本号、说明、加载的程序集等）的属性。|  
|`My.Application.Log` \(<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log%2A>\)|提供一个属性和多个方法，以将事件和异常信息写入应用程序的日志侦听器。|  
|`My.Computer` \(<xref:Microsoft.VisualBasic.Devices.Computer>\)|提供用于操作计算机组件（例如音频、时钟、键盘、文件系统等）的属性。|  
|`My.Computer.Audio` \(<xref:Microsoft.VisualBasic.Devices.Audio>\)|提供用于播放声音的方法。|  
|`My.Computer.Clipboard` \(<xref:Microsoft.VisualBasic.Devices.Computer.Clipboard%2A>\)|提供操作剪贴板的方法。|  
|`My.Computer.Clock` \(<xref:Microsoft.VisualBasic.Devices.Clock>\)|提供用于从系统时钟访问当前的本地时间和协调通用时间（与格林尼治标准时间相同）的属性。|  
|`My.Computer.FileSystem` \(<xref:Microsoft.VisualBasic.FileIO.FileSystem>\)|提供用于处理驱动器、文件和目录的属性和方法。|  
|`My.Computer.FileSystem.SpecialDirectories` \(<xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>\)|提供用于访问经常引用的目录的属性。|  
|`My.Computer.Info` \(<xref:Microsoft.VisualBasic.Devices.ComputerInfo>\)|提供用于获取与计算机的内存、已加载程序集、名称和操作系统有关的信息的属性。|  
|`My.Computer.Keyboard` \(<xref:Microsoft.VisualBasic.Devices.Keyboard>\)|提供了用于访问键盘当前状态（例如，当前按下了什么键）的属性，并提供了向活动窗口发送键击的方法。|  
|`My.Computer.Mouse` \(<xref:Microsoft.VisualBasic.Devices.Mouse>\)|提供用于获取有关安装在本地计算机上的鼠标的格式和配置信息的属性。|  
|`My.Computer.Network` \(<xref:Microsoft.VisualBasic.Devices.Network>\)|提供用于与计算机所连接的网络进行交互的属性、事件和方法。|  
|`My.Computer.Ports` \(<xref:Microsoft.VisualBasic.Devices.Ports>\)|提供用于访问计算机的串行端口的属性和方法。|  
|`My.Computer.Registry` \(<xref:Microsoft.VisualBasic.MyServices.RegistryProxy>\)|提供操作注册表的属性和方法。|  
|[My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)|提供属性，用于访问在当前项目中声明的每个 Windows 窗体的实例。|  
|`My.Log` \(<xref:Microsoft.VisualBasic.Logging.AspLog>\)|提供用于将事件和异常信息写入 Web 应用程序的应用程序日志侦听器的属性和方法。|  
|[My.Request 对象](../../../visual-basic/language-reference/objects/my-request-object.md)|获取请求的页的 <xref:System.Web.HttpRequest> 对象。  `My.Request` 对象包含有关当前 HTTP 请求的信息。<br /><br /> `My.Request` 对象仅可用于 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 应用程序。|  
|[My.Resources 对象](../../../visual-basic/language-reference/objects/my-resources-object.md)|提供用于访问应用程序资源的属性和类。|  
|[My.Response 对象](../../../visual-basic/language-reference/objects/my-response-object.md)|获取与 <xref:System.Web.UI.Page> 关联的 <xref:System.Web.HttpResponse> 对象。  该对象使您得以将 HTTP 响应数据发送到客户端，并包含有关该响应的信息。<br /><br /> `My.Response` 对象仅可用于 [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] 应用程序。|  
|[My.Settings 对象](../../../visual-basic/language-reference/objects/my-settings-object.md)|提供用于访问应用程序设置的属性和方法。|  
|`My.User` \(<xref:Microsoft.VisualBasic.ApplicationServices.User>\)|提供对有关当前用户的信息的访问。|  
|[My.WebServices 对象](../../../visual-basic/language-reference/objects/my-webservices-object.md)|提供属性，用于创建和访问当前项目引用的每个 Web 服务的单个实例。|  
|<xref:Microsoft.VisualBasic.FileIO.TextFieldParser>|提供分析结构化文本文件的方法和属性。|  
  
## 请参阅  
 [Visual Basic 语言参考](../../../visual-basic/language-reference/index.md)   
 [Visual Basic](../../../visual-basic/index.md)