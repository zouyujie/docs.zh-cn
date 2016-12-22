---
title: "部署引用 Power Pack 控件的应用程序 (Visual Studio) | Microsoft Docs"
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
  - "Power Pack, 部署"
ms.assetid: f2230f53-a745-4731-89e6-033943faa209
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 部署引用 Power Pack 控件的应用程序 (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

如果要部署引用 Power Pack 控件（<xref:Microsoft.VisualBasic.PowerPacks.LineShape>、<xref:Microsoft.VisualBasic.PowerPacks.OvalShape>、<xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> 或 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>）的应用程序，必须在目标计算机上安装这些控件。  
  
## 作为系统必备组件安装 Power Pack 控件  
 若要成功部署应用程序，还必须部署该应用程序引用的全部组件。  安装系统必备组件的过程称为“引导”。  
  
 在开发计算机上安装 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 时，会将一个 Power Pack 引导程序包添加到 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 引导程序目录中。  当按照这些步骤为 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] 或 Windows Installer 部署添加系统必备时，便可使用此包。  
  
 默认情况下，引导组件和安装包的部署位置相同。  您也可以选择从 URL 或文件共享位置部署这些组件，用户在需要时可从该 URL 或文件共享位置下载这些组件。  
  
> [!NOTE]
>  若要安装引导的组件，用户可能需要对计算机拥有管理权限或类似用户权限。  对于 [!INCLUDE[ndptecclick](../../../visual-basic/developing-apps/printing/includes/ndptecclick_md.md)] 应用程序，这意味着无论该应用程序指定的安全级别如何，用户都需要拥有管理权限才能安装它。  在安装应用程序之后，用户无需管理权限即可运行该应用程序。  
  
 安装期间，如果目标计算机上没有 Power Pack 控件，系统会提示用户安装这些控件。  
  
 作为引导方法的一种替代方法，可以使用电子软件分发系统（如 Microsoft Systems Management Server）预先部署 Power Pack 控件。  
  
## 请参阅  
 [How to: Install Prerequisites in Windows Installer Deployment](http://msdn.microsoft.com/zh-cn/653fc868-2486-429c-b75e-2f9d0c7f6619)   
 [如何：与 ClickOnce 应用程序一起安装系统必备组件](../Topic/How%20to:%20Install%20Prerequisites%20with%20a%20ClickOnce%20Application.md)   
 [选择部署策略](http://msdn.microsoft.com/zh-cn/ecd632d8-063c-4028-b785-81bba045107b)   
 [Visual Basic Power Pack 控件](../../../visual-basic/developing-apps/windows-forms/power-packs-controls.md)