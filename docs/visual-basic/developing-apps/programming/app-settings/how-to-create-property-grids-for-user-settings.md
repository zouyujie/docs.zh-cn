---
title: "如何：在 Visual Basic 中创建用户设置的属性网格 | Microsoft Docs"
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
  - "My.Settings 对象, 为用户设置创建属性网格"
  - "属性网格"
  - "属性网格, 为用户设置创建"
  - "用户设置, 创建属性网格"
ms.assetid: b0bc737e-50d1-43d1-a6df-268db6e6f91c
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：在 Visual Basic 中创建用户设置的属性网格
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过用 `My.Settings` 对象的用户设置属性填充 <xref:System.Windows.Forms.PropertyGrid> 控件，可以创建用户设置的属性网格。  
  
> [!NOTE]
>  若要使此示例正确运行，您的应用程序必须配置用户设置。  有关更多信息，请参见[管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)。  
  
 `My.Settings` 对象将每个设置公开为一个属性。  属性名称就是设置的名称，属性类型就是设置类型。  设置的**“范围”**确定属性是否为只读；**“应用程序”**范围设置的属性为只读，而**“用户”**范围设置的属性为读写。  有关更多信息，请参见[My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)。  
  
> [!NOTE]
>  不能在运行时更改或保存应用程序范围的设置的值。  只有在创建应用程序（通过**“项目设计器”**）或编辑应用程序的配置文件时才能更改应用程序范围的设置。  有关更多信息，请参见[管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)。  
  
 此示例使用 <xref:System.Windows.Forms.PropertyGrid> 控件访问 `My.Settings` 对象的用户设置属性。  默认情况下，<xref:System.Windows.Forms.PropertyGrid> 显示 `My.Settings` 对象的所有属性。  但用户设置属性具有 <xref:System.Configuration.UserScopedSettingAttribute> 特性。  此示例将 <xref:System.Windows.Forms.PropertyGrid> 的 <xref:System.Windows.Forms.PropertyGrid.BrowsableAttributes%2A> 属性设置为 <xref:System.Configuration.UserScopedSettingAttribute>，以便只显示用户设置属性。  
  
### 添加用户设置属性网格  
  
1.  将**“PropertyGrid”**控件从**“工具箱”**添加到应用程序的设计图面上（假定此时位于  `Form1` 上）。  
  
     该属性网格控件的默认名称为 `PropertyGrid1`。  
  
2.  双击 `Form1` 的设计图面以打开窗体加载事件处理程序的代码。  
  
3.  将 `My.Settings` 对象设置为属性网格的选定对象。  
  
     [!code-vb[VbVbalrMyResources#11](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#11)]  
  
4.  将属性网格配置为只显示用户设置。  
  
     [!code-vb[VbVbalrMyResources#12](../../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#12)]  
  
    > [!NOTE]
    >  若要只显示应用程序范围的设置，请使用 <xref:System.Configuration.ApplicationScopedSettingAttribute> 属性而不是 <xref:System.Configuration.UserScopedSettingAttribute>。  
  
## 可靠编程  
 应用程序在关闭时会保存用户设置。  若要立即保存设置，请调用 `My.Settings.Save` 方法。  有关更多信息，请参见[如何：在 Visual Basic 中保存用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)。  
  
## 请参阅  
 [My.Settings 对象](../../../../visual-basic/language-reference/objects/my-settings-object.md)   
 [如何：在 Visual Basic 中读取应用程序设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [如何：在 Visual Basic 中更改用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [如何：在 Visual Basic 中保存用户设置](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [管理应用程序设置 \(.NET\)](/visual-studio/ide/managing-application-settings-dotnet)