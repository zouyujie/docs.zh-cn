---
title: "使用 My 开发 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.MyWpfExtension.Windows"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My 功能"
  - "My 命名空间"
  - "My 对象"
  - "Visual Basic, 编程"
ms.assetid: f1d04509-5e46-4551-9f9f-94334a121fca
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# 使用 My 开发 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Visual Basic 提供了供快速开发应用程序使用的新功能，这些新功能不仅功能强大，还提高了生产效率和易用性。  其中一种功能称为 `My`，通过它可以访问与应用程序及其运行时环境相关的信息和默认对象实例。  此信息的组织格式可以使 IntelliSense 发现它并根据用途对其进行逻辑描述。  
  
 `My` 的顶级成员作为对象公开。  每个对象的行为都与具有 `Shared` 成员的命名空间或类相似，并可公开一组相关成员。  
  
 此表显示顶级 `My` 对象及其相互之间的关系。  
  
 ![My 的对象模型](../../../visual-basic/developing-apps/development-with-my/media/myobjmodel.png "MyObjModel")  
  
## 本节内容  
 [使用 My.Application、My.Computer 和 My.User 执行任务](../../../visual-basic/developing-apps/development-with-my/performing-tasks-with-my-application-my-computer-and-my-user.md)  
 描述三个重要的 `My` 对象：`My.Application`、`My.Computer` 和 `My.User`，通过它们可以访问信息和功能。  
  
 [My.Forms 和 My.WebServices 提供的默认对象实例](../../../visual-basic/developing-apps/development-with-my/default-object-instances-provided-by-my-forms-and-my-webservices.md)  
 描述 `My.Forms` 和 `My.WebServices` 对象，通过它们可以访问应用程序所使用的窗体、数据源和 XML Web services。  
  
 [使用 My.Resources 和 My.Settings 快速开发应用程序](../../../visual-basic/developing-apps/development-with-my/rapid-application-development-with-my-resources-and-my-settings.md)  
 描述 `My.Resources` 和 `My.Settings` 对象，通过它们可以访问应用程序的资源和设置。  
  
 [Visual Basic 应用程序模型概述](../../../visual-basic/developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)  
 描述 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 应用程序的启动\/关闭模型。  
  
 [My 对项目类型的依赖方式](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)  
 详细描述不同的项目类型都提供哪些 `My` 功能。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [My.WebServices 对象](../../../visual-basic/language-reference/objects/my-webservices-object.md)   
 [My 对项目类型的依赖方式](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)