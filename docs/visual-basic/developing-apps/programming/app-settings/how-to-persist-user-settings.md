---
title: "如何：在 Visual Basic 中保存用户设置 | Microsoft Docs"
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
  - "My.Settings 对象, 保持用户设置"
  - "持久性, 保持用户设置 [Visual Basic]"
  - "用户设置, 保持"
ms.assetid: 0e5e6415-b6e2-4602-9be0-a65fa167d007
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中保存用户设置
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

您可以使用 `My.Settings.Save` 方法保存对用户设置的更改。  
  
 通常，应用程序设计为在关闭时保存对用户设置的更改。  这是因为保存设置需要花费几秒钟的时间（具体取决于几个因素）。  
  
 有关更多信息，请参见[My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)。  
  
> [!NOTE]
>  虽然在运行时可以更改并保存用户范围设置值，但应用程序范围设置是只读的，不可以通过编程方式进行更改。  创建应用程序时，通过**“项目设计器”**或通过编辑应用程序的配置文件，可更改应用程序范围设置。  有关更多信息，请参见[管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)。  
  
## 示例  
 此示例更改 `LastChanged` 用户设置的值，并调用 `My.Settings.Save` 方法保存所做的更改。  
  
 [!code-vb[VbVbalrMyResources#5](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-persist-user-settings_1.vb)]  
  
 若要使此示例正常工作，应用程序必须具有类型为 `Date` 的 `LastChanged` 用户设置。  有关更多信息，请参见[管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)。  
  
## 请参阅  
 [My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [如何：在 Visual Basic 中读取应用程序设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [如何：在 Visual Basic 中更改用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [如何：在 Visual Basic 中创建用户设置的属性网格](../Topic/How%20to:%20Create%20Property%20Grids%20for%20User%20Settings%20in%20Visual%20Basic.md)   
 [管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)