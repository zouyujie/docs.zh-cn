---
title: "如何：使用两个 DataRepeater 控件创建主/详细信息窗体 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 主/详细信息表"
ms.assetid: eec43ae3-05d8-45a1-8d41-3803c6359dbe
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 如何：使用两个 DataRepeater 控件创建主/详细信息窗体 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

您可以通过使用两个或更多个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件创建主\/详细信息窗体来显示相关数据。  例如，您可能希望在一个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 中显示一个客户列表，当用户选择某个客户时，在第二个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 中显示该客户的订单列表。  
  
 您可以通过将共享相同主表节点的详细信息项从**“数据源”**窗口中拖到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中来显示相关数据。  例如，如果您的数据源有一个 Customers 表和一个相关的 Orders 表，那么在**“数据源”**窗口中，您会看到这两个表在树视图中均显示为顶级节点。  展开 Customers 节点以便您能看到各个列。  请注意，列表中的最后一列是一个可展开节点，表示 Orders 表。  此节点表示客户的相关订单。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 在两个 DataRepeater 控件中显示相关数据  
  
1.  从**“工具箱”**的**“Visual Basic PowerPacks”**选项卡中将两个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件拖到窗体或容器控件中。  
  
2.  拖动大小调整控点和定位控点来调整这两个控件的大小并将它们并列放置在一起。  
  
3.  在**“数据”**菜单上，单击**“显示数据源”**。  
  
    > [!NOTE]
    >  如果**“数据源”**窗口是空的，请在该窗口中添加一个数据源。  有关更多信息，请参见 [数据源概述](/visual-studio/data-tools/add-new-data-sources)。  
  
4.  在**“数据源”**窗口中选择主表的顶级节点。  
  
5.  通过单击表节点上的下拉列表中的**“详细信息”**将主表的下拉类型更改为“详细信息”。  
  
6.  将主表节点拖到第一个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板区域。  
  
7.  展开主表节点并选择相关表的详细信息节点。  
  
8.  通过单击表节点上的下拉列表中的**“详细信息”**将详细信息表的下拉类型更改为“详细信息”。  
  
9. 选择此表节点并将它拖到第二个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板区域。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [如何：在 Windows 窗体应用程序中显示相关数据](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md)   
 [如何：更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)