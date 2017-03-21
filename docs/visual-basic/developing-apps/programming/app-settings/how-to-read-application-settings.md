---
title: "如何：在 Visual Basic 中读取应用程序设置 | Microsoft Docs"
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
  - "应用程序设置, 读取"
  - "My.Settings 对象, 读取应用程序设置"
  - "读取应用程序设置"
ms.assetid: eb3428ef-115e-49a8-a878-e0613183fee0
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 如何：在 Visual Basic 中读取应用程序设置
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

您可以通过访问 `My.Settings` 对象上用户设置的属性来读取该设置。  
  
 `My.Settings` 对象将每个设置公开为一个属性。  属性名称就是设置的名称，属性类型就是设置类型。  设置的**“范围”**指示属性是否为只读的；**“应用程序”**范围设置的属性是只读的，而**“用户”**范围设置的属性是读\/写的。  有关更多信息，请参见[My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)。  
  
## 示例  
 此示例显示 `Nickname` 设置的值。  
  
 [!code-vb[VbVbalrMyResources#14](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/how-to-read-application-settings_1.vb)]  
  
 若要使此示例正常工作，应用程序必须具有类型为 `String` 的 `Nickname` 设置。  有关更多信息，请参见[管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)。  
  
## 请参阅  
 [My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [如何：在 Visual Basic 中更改用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [如何：在 Visual Basic 中保存用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [如何：在 Visual Basic 中创建用户设置的属性网格](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)