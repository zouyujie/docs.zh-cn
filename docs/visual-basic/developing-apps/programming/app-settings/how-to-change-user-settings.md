---
title: "如何：在 Visual Basic 中更改用户设置 | Microsoft Docs"
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
  - "示例 [Visual Basic], 更改用户设置"
  - "My.Settings 对象, 更改用户设置"
  - "用户设置"
  - "用户设置, 在 Visual Basic 中更改"
ms.assetid: 41250181-c594-4854-9988-8183b9eb03cf
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中更改用户设置
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

您可以通过在 `My.Settings` 对象上为用户设置的属性赋予新值来更改该设置。  
  
 `My.Settings` 对象将每个设置公开为一个属性。  属性名称就是设置的名称，属性类型就是设置类型。  设置的**“范围”**确定属性是否为只读：**“应用程序”**范围设置的属性为只读，而**“用户”**范围设置的属性为读写。  有关更多信息，请参见[My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)。  
  
> [!NOTE]
>  虽然在运行时可以更改并保存用户范围设置值，但应用程序范围设置是只读的，不可以通过编程方式进行更改。  创建应用程序时，可以通过使用**“项目设计器”**或编辑应用程序的配置文件，来更改应用程序范围设置。  有关更多信息，请参见[管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)。  
  
## 示例  
 此示例更改 `Nickname` 用户设置的值。  
  
 [!code-vb[VbVbalrMyResources#7](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-change-user-settings_1.vb)]  
  
 若要使此示例正常工作，应用程序必须具有类型为 `String` 的 `Nickname` 用户设置。  
  
 应用程序在关闭时会保存用户设置。  若要立即保存设置，请调用 `My.Settings.Save` 方法。  有关更多信息，请参见[如何：在 Visual Basic 中保存用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)。  
  
## 请参阅  
 [My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [如何：在 Visual Basic 中读取应用程序设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [如何：在 Visual Basic 中保存用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [如何：在 Visual Basic 中创建用户设置的属性网格](../Topic/How%20to:%20Create%20Property%20Grids%20for%20User%20Settings%20in%20Visual%20Basic.md)   
 [管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)