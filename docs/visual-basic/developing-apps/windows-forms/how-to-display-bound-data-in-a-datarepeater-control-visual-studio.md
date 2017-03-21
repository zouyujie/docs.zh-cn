---
title: "如何：在 DataRepeater 控件中显示绑定数据 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 数据绑定"
  - "DataRepeater, 显示绑定控件"
ms.assetid: 56a15326-1334-4275-af4e-075cad79e6f7
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：在 DataRepeater 控件中显示绑定数据 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件最常见的用途是显示来自数据库或其他数据源的绑定数据。  
  
 除了绑定控件外，您可能还希望添加其他控件，例如在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的每个项上重复的静态标签或图像。  有关更多信息，请参见 [如何：在 DataRepeater 控件中显示未绑定的控件](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)。  
  
 还可以通过将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> 属性设置为 `True` 并将数据源分配到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DataSource%2A> 属性，从而在运行时绑定到数据源。  在这种情况下，将需要管理与数据源的所有交互。  有关更多信息，请参见 [DataRepeater 控件中的虚拟模式](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md)。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 创建数据绑定的 DataRepeater  
  
1.  从**“工具箱”**的**“Visual Basic PowerPacks”**选项卡中将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件拖到窗体或容器控件中。  
  
2.  拖动大小调整控点和定位控点来调整该控件的大小以及定位该控件。  
  
     请注意，该控件有两个矩形区域。  上半部分区域是项模板；添加到该模板中的控件将在运行时在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的每个项中重复。  下半部分区域是视区，项显示在该区域。  
  
     您还可以通过在“属性”窗口中更改**“Size”**和**“Position”**属性来调整控件或项模板的大小或对它们进行定位。  
  
3.  在**“数据”**菜单上，单击**“显示数据源”**。  
  
    > [!NOTE]
    >  如果**“数据源”**窗口是空的，请在该窗口中添加一个数据源。  有关更多信息，请参见 [数据源概述](/visual-studio/data-tools/add-new-data-sources)。  
  
4.  在**“数据源”**窗口中，选择您要绑定的数据所在表的顶级节点。  
  
5.  通过单击表节点上的下拉列表中的 `Details` 将该表的下拉类型更改为 `Details`。  
  
6.  选择该表节点，将它拖到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板区域。  
  
     您可以指定要为每个字段显示的控件类型。  有关更多信息，请参见[设置从“数据源”窗口中拖动时要创建的控件](/visual-studio/data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示未绑定的控件](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [如何：使用两个 DataRepeater 控件创建主\/详细信息窗体](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [如何：更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)