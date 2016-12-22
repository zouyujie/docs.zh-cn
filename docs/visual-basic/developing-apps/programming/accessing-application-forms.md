---
title: "访问应用程序窗体 (Visual Basic) | Microsoft Docs"
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
  - "应用程序窗体, 访问"
  - "窗体, 访问所有打开的"
  - "窗体, 从一个窗体访问另一个窗体"
  - "窗体, 通信"
  - "My.Forms 对象"
ms.assetid: 9aaf5aaf-2012-4f97-89c7-6e62b9d17863
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 访问应用程序窗体 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`My.Forms` 对象为应用程序项目中声明的每个 Windows 窗体的实例提供了一种简单的访问方法。  也可以使用 `My.Application` 对象的属性访问应用程序的初始屏幕和主窗体，并获取应用程序的已打开窗体的列表。  
  
## 任务  
 下表列出的示例演示如何访问应用程序的窗体。  
  
|||  
|-|-|  
|若要|请参见|  
|从应用程序中的一个窗体访问另一个窗体。|[My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)|  
|显示应用程序的所有打开的窗体的标题。|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>|  
|在应用程序启动时用状态信息更新初始屏幕。|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A>|  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OpenForms%2A>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A>   
 [My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)