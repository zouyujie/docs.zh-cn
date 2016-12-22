---
title: "DataRepeater 控件简介 (Visual Studio) | Microsoft Docs"
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
  - "DataRepeater"
  - "DataRepeater, 概述"
  - "重复数据"
ms.assetid: 78a52a1d-65f0-4ecb-97ff-53bc114300c5
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# DataRepeater 控件简介 (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Visual Basic Power Pack <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件是显示重复数据（例如，数据库表中的行）的控件的可滚动容器。  当您需要进一步控制数据的布局时，可用它来取代 <xref:System.Windows.Forms.DataGridView> 控件。  <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 通过在一个滚动视图中创建多个实例来“重复”一组相关控件。  这使用户可同时查看多条记录。  
  
## 概述  
 设计时，<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件包含两个部分。  外层区域是视区，运行时滚动数据将显示在该区域。  内层（顶部）区域称为项模板，将在运行时重复的控件放置在该区域，通常一个控件对应于数据源中的一个字段。  项模板中的属性和控件封装在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 属性中。  
  
 运行时，<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 复制到虚拟 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 对象中，该对象用于显示在每条记录滚动到视图中时的数据。  您可以在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件中自定义各条记录的显示，例如基于字段所包含的值突出显示该字段。  有关更多信息，请参见 [如何：更改 DataRepeater 控件的外观](../Topic/How%20to:%20Change%20the%20Appearance%20of%20a%20DataRepeater%20Control%20\(Visual%20Studio\).md)。  
  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件最常见的用途是显示数据表或其他绑定数据源中的数据。  除了 [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] 数据对象外，还可以将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件绑定到任何实现 <xref:System.Collections.IList> 接口（包括数组）的类、任何实现 <xref:System.ComponentModel.IListSource> 接口的类、任何实现 <xref:System.ComponentModel.IBindingList> 接口的类或任何实现 <xref:System.ComponentModel.IBindingListView> 接口的类。  
  
### 数据绑定  
 通常情况下，通过将字段从**“数据源”**窗口拖到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件来完成数据绑定。  有关更多信息，请参见 [如何：在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)。  
  
 处理大量数据时，可以将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> 属性设置为 `True` 来显示可用数据的子集。  虚拟模式要求实现从中填充 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 的数据缓存，并且您必须在运行时控制与数据缓存的所有交互。  有关更多信息，请参见 [DataRepeater 控件中的虚拟模式](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md)。  
  
 您还可以在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件上显示未绑定的控件。  例如，可以显示在每个项上都重复的图像。  有关更多信息，请参见 [如何：在 DataRepeater 控件中显示未绑定的控件](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)。  
  
### 事件  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件最重要的事件是 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件和 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged> 事件，前者在新项滚动到视图中时引发，后者在选择项时引发。  您可以使用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件来更改项的外观。  例如，可以突出显示负值。  使用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged> 事件访问选中某项时控件的值。  
  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件在代码编辑器中公开所有标准的控件事件。  但是，不应该使用其中某些事件。  运行时将不会引发键盘和鼠标事件，如 `KeyDown`、`Click` 和 `MouseDown`，因为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件自身从来都不会有焦点。  
  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 不会在设计时公开事件，因为它只能在运行时创建。  如果希望处理键盘和鼠标事件，可以在运行时将 <xref:System.Windows.Forms.Panel> 控件添加到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>，然后处理 <xref:System.Windows.Forms.Panel> 的事件。  有关更多信息，请参见 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)。  
  
### 自定义  
 可通过多种方法在运行时和设计时自定义 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的外观和行为。  可以设置属性来更改颜色、隐藏或修改项标头以及将方向从垂直改为水平等。  有关更多信息，请参见[如何：更改 DataRepeater 控件的外观](../Topic/How%20to:%20Change%20the%20Appearance%20of%20a%20DataRepeater%20Control%20\(Visual%20Studio\).md)、[如何：在 DataRepeater 控件中显示项标题](../Topic/How%20to:%20Display%20Item%20Headers%20in%20a%20DataRepeater%20Control%20\(Visual%20Studio\).md)和[如何：更改 DataRepeater 控件的布局](../Topic/How%20to:%20Change%20the%20Layout%20of%20a%20DataRepeater%20Control%20\(Visual%20Studio\).md)。  
  
 请注意，有些属性适用于 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件自身，而有些属性则仅适用于 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>。  请确保在设置属性前选择了控件的正确部分。  有关更多信息，请参见 [如何：更改 DataRepeater 控件的外观](../Topic/How%20to:%20Change%20the%20Appearance%20of%20a%20DataRepeater%20Control%20\(Visual%20Studio\).md)。  
  
 其他自定义包括控制添加或删除记录的能力、添加搜索功能以及以主格式和详细信息格式显示相关数据。  有关更多信息，请参见[如何：禁止添加和删除 DataRepeater 项](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)、[如何：在 DataRepeater 控件中搜索数据](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md) 和[如何：使用两个 DataRepeater 控件创建主\/详细信息窗体](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)。  
  
## 请参阅  
 [DataRepeater 控件](../../../visual-basic/developing-apps/windows-forms/datarepeater-control-visual-studio.md)   
 [演练：在 DataRepeater 控件中显示数据](../Topic/Walkthrough:%20Displaying%20Data%20in%20a%20DataRepeater%20Control%20\(Visual%20Studio\).md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)