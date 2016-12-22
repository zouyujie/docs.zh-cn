---
title: "自定义 My 中可用的对象 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "My 命名空间"
  - "My 命名空间, 自定义"
ms.assetid: 4e8279c2-ed5b-4681-8903-8a6671874000
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 自定义 My 中可用的对象 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本主题描述了如何通过设置项目的 `_MYTYPE` 条件编译常数来控制启用哪些 `My` 对象。  [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 集成开发环境 \(IDE\) 使项目的 `_MYTYPE` 条件编译常数与项目的类型保持同步。  
  
## 预定义的 \_MYTYPE 值  
 必须使用 `/define` 编译器选项设置 `_MYTYPE` 条件编译常数。  当为 `_MYTYPE` 常数指定自己的值时，必须使用反斜杠\/引号 \(\\"\) 序列将字符串值引起来。  例如，您可以使用：  
  
```  
/define:_MYTYPE=\"WindowsForms\"  
```  
  
 此表显示为几种项目类型设置的 `_MYTYPE` 条件编译常数。  
  
|项目类型|\_MYTYPE 值|  
|----------|----------------|  
|类库|"Windows"|  
|控制台应用程序|"Console"|  
|Web|"Web"|  
|Web 控件库|"WebControl"|  
|Windows 应用程序|"WindowsForms"|  
|Windows 应用程序，当使用自定义的 `Sub Main` 启动时|"WindowsFormsWithCustomSubMain"|  
|Windows 控件库|"Windows"|  
|Windows 服务|"Console"|  
|空|"Empty"|  
  
> [!NOTE]
>  所有的条件编译字符串比较都区分大小写，而无论 `Option Compare` 语句如何设置。  
  
## 相关 \_MY 编译常数  
 而 `_MYTYPE` 条件编译常数控制其他几个 `_MY` 编译常数的值：  
  
|\_MYTYPE|\_MYAPPLICATIONTYPE|\_MYCOMPUTERTYPE|\_MYFORMS|\_MYUSERTYPE|\_MYWEBSERVICES|  
|--------------|-------------------------|----------------------|---------------|------------------|---------------------|  
|"Console"|"Console"|"Windows"|未定义|"Windows"|TRUE|  
|"Custom"|未定义|未定义|未定义|未定义|未定义|  
|"Empty"|未定义|未定义|未定义|未定义|未定义|  
|"Web"|未定义|"Web"|FALSE|"Web"|FALSE|  
|"WebControl"|未定义|"Web"|FALSE|"Web"|TRUE|  
|"Windows" 或 ""|"Windows"|"Windows"|未定义|"Windows"|TRUE|  
|"WindowsForms"|"WindowsForms"|"Windows"|TRUE|"Windows"|TRUE|  
|"WindowsFormsWithCustomSubMain"|"Console"|"Windows"|TRUE|"Windows"|TRUE|  
  
 默认情况下，未定义的条件编译常数将解析为 `FALSE`。  当编译项目以重写默认行为时，您可以为未定义的常数指定值。  
  
> [!NOTE]
>  当 `_MYTYPE` 设置为 "Custom" 时，项目包含 `My` 命名空间，但不包含对象。  不过，将 `_MYTYPE` 设置为 "Empty" 可防止编译器添加 `My` 命名空间及其对象。  
  
 此表描述 `_MY` 编译常数的预定义值的效果。  
  
|常量|含义|  
|--------|--------|  
|`_MYAPPLICATIONTYPE`|如果常数为 "Console"、"Windows" 或 "WindowsForms"，则启用 `My.Application`：<br /><br /> -   "Console" 版本从 <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> 中派生，  而且其成员比 "Windows" 版本要少。<br />-   "Windows" 版本从 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase> 中派生，而且其成员比 "WindowsForms" 版本要少。<br />-   `My.Application` 的 "WindowsForms" 版本从 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 中派生。  如果将 `TARGET` 常数定义为 "winexe"，则该类包含 `Sub Main` 方法。|  
|`_MYCOMPUTERTYPE`|如果常数为 "Web" 或 "Windows"，则启用 `My.Computer`：<br /><br /> -   "Web" 版本从 <xref:Microsoft.VisualBasic.Devices.ServerComputer> 中派生，而且其成员比 "Windows" 版本要少。<br />-   `My.Computer` 的 "Windows" 版本从 <xref:Microsoft.VisualBasic.Devices.Computer> 中派生。|  
|`_MYFORMS`|如果常数为 `TRUE`，则启用 `My.Forms`。|  
|`_MYUSERTYPE`|如果常数为 "Web" 或 "Windows"，则启用 `My.User`：<br /><br /> -   `My.User` 的 "Web" 版本与当前 HTTP 请求的用户标识相关联。<br />-   `My.User` 的 "Windows" 版本与线程的当前主体相关联。|  
|`_MYWEBSERVICES`|如果常数为 `TRUE`，则启用 `My.WebServices`。|  
|`_MYTYPE`|如果常数为 "Web"，则启用 `My.Log`、`My.Request` 和 `My.Response`。|  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.Logging.Log>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [My 对项目类型的依赖方式](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)   
 [My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [My.Request 对象](../../../visual-basic/language-reference/objects/my-request-object.md)   
 [My.Response 对象](../../../visual-basic/language-reference/objects/my-response-object.md)   
 [My.WebServices 对象](../../../visual-basic/language-reference/objects/my-webservices-object.md)