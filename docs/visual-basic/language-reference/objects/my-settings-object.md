---
title: "My.Settings 对象 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "My.MySettingsProperty.Settings"
  - "My.Settings"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Settings 对象"
ms.assetid: 41f30dc1-202a-4273-b9b7-5728941f996c
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# My.Settings 对象
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

提供属性和方法来访问应用程序的设置。  
  
## <a name="remarks"></a>备注  
  `My.Settings` 对象提供对应用程序的设置的访问，并允许您动态地存储和检索属性设置和您的应用程序的其他信息。 有关详细信息，请参阅 [管理应用程序设置 (.NET)](/visual-studio/ide/managing-application-settings-dotnet)。  
  
## <a name="properties"></a>属性  
 属性的 `My.Settings` 对象提供对应用程序的设置的访问。 若要添加或删除设置，请使用 **设置设计器**。  
  
 每个设置具有 **名称**, ，**类型**, ，**范围**, ，和 **值**, ，并且这些设置确定用于访问每个设置的属性中的显示方式 `My.Settings` 对象︰  
  
-   **名称** 确定该属性的名称。  
  
-   **类型** 确定该属性的类型。  
  
-   **作用域** 指示属性是否是只读的。 如果值为 **应用程序**, ，该属性是只读的; 如果值为 **用户**, ，该属性是可读写。  
  
-   **值** 是属性的默认值。  
  
## <a name="methods"></a>方法  
  
|||  
|-|-|  
|方法|描述|  
|`Reload`|重新加载上次保存的值中的用户设置。|  
|`Save`|将保存当前的用户设置。|  
  
  `My.Settings` 对象还提供了高级的属性和方法，继承自 <xref:System.Configuration.ApplicationSettingsBase> 类。  
  
## <a name="tasks"></a>任务  
 下表列出了所涉及的任务的示例 `My.Settings` 对象。  
  
|||  
|-|-|  
|到|请参阅|  
|读取应用程序设置|[如何︰ 读取在 Visual Basic 中的应用程序设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)|  
|更改用户设置|[如何︰ 在 Visual Basic 中的用户设置更改](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)|  
|保持用户设置|[如何︰ 保存在 Visual Basic 中的用户设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)|  
|创建用户设置的属性网格|[如何︰ 创建在 Visual Basic 中的用户设置的属性网格](../Topic/How%20to:%20Create%20Property%20Grids%20for%20User%20Settings%20in%20Visual%20Basic.md)|  
  
## <a name="example"></a>示例  
 此示例中显示的值 `Nickname` 设置。  
  
 [!code-vb[VbVbalrMyResources#14](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-settings-object_1.vb)]  
  
 对于此示例正常工作，您的应用程序必须具有 `Nickname` 类型设置 `String`。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Configuration.ApplicationSettingsBase>   
 [如何︰ 读取在 Visual Basic 中的应用程序设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [如何︰ 在 Visual Basic 中的用户设置更改](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [如何︰ 保存在 Visual Basic 中的用户设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [如何︰ 创建在 Visual Basic 中的用户设置的属性网格](../Topic/How%20to:%20Create%20Property%20Grids%20for%20User%20Settings%20in%20Visual%20Basic.md)   
 [管理应用程序设置 (.NET)](/visual-studio/ide/managing-application-settings-dotnet)