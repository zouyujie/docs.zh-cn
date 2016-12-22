---
title: "DataRepeater 控件中的虚拟模式 (Visual Studio) | Microsoft Docs"
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
  - "DataRepeater"
  - "DataRepeater, 虚拟模式"
  - "虚拟数据绑定"
ms.assetid: 5fb805dc-2d8b-4139-b1e3-86e4c2667221
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# DataRepeater 控件中的虚拟模式 (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

如果要在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中显示大量表格数据，可通过将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> 属性设置为 `True` 并显式管理该控件与其数据源的交互来提高性能。  <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件提供若干事件，您可以处理这些事件来与数据源交互并根据需要在运行时显示数据。  
  
## 虚拟模式的工作原理  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件最常见的用法是在设计时将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 的子控件绑定到数据源并使 <xref:System.Windows.Forms.BindingSource> 可以根据需要来回传递数据。  使用虚拟模式时，控件不绑定到数据源，数据在运行时传入或传出底层数据源。  
  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> 属性设置为 `True` 时，您可以通过从**“工具箱”**添加控件来创建用户界面，而不从**“数据源”**窗口添加绑定控件。  
  
 事件的引发是基于控件的，并且您必须添加代码来处理数据的显示。  当某个新的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 滚动到视图中时，将为每个控件引发一次 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> 事件，因此您必须在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> 事件处理程序中为每个控件提供值。  
  
 如果用户更改了某个控件中的数据，将引发 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> 事件，因此您必须验证数据并将它保存到数据源中。  
  
 如果用户添加新项，将引发 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded> 事件。  使用此事件的处理程序在数据源中创建新记录。  若要防止意外更改，还必须监视每个控件的 <xref:System.Windows.Forms.Control.KeyDown> 事件，并在用户按 Esc 键时调用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A>。  
  
 如果数据源发生更改，则可通过调用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetTemplateItem%2A> 和 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetTemplateItem%2A> 方法来刷新 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件。  必须按顺序调用这两种方法。  
  
 最后，您还必须实现 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved> 事件的事件处理程序，该事件在删除项时发生；还可以选择实现 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletingItems> 和 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletedItems> 事件的事件处理程序，这两个事件在用户通过按 Delete 键删除项时发生。  
  
## 实现虚拟模式  
 下面是实现虚拟模式所需的步骤。  
  
#### 实现虚拟模式  
  
1.  从**“工具箱”**的**“Visual Basic PowerPacks”**选项卡中将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件拖到窗体或容器控件中。  将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> 属性设置为 `True`。  
  
2.  从**“工具箱”**中将控件拖到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板区域（上半部分区域）。  您需要为数据源中要显示的每个字段分别添加一个控件。  
  
3.  为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> 事件实现一个处理程序以便为每个控件提供值。  此事件在某个新的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 滚动到视图中时引发。  代码与下面的示例类似，此示例针对一个名为 `Employees` 的数据源。  
  
     [!CODE [VbPowerPacksDataRepeaterVirtualMode#1](../CodeSnippet/VS_Snippets_VBCSharp/VbPowerPacksDataRepeaterVirtualMode#1)]  
  
4.  为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> 事件实现一个处理程序来存储数据。  此事件在用户将更改提交到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 的子控件时引发。  代码与下面的示例类似，此示例针对一个名为 `Employees` 的数据源。  
  
     [!CODE [VbPowerPacksDataRepeaterVirtualMode#2](../CodeSnippet/VS_Snippets_VBCSharp/VbPowerPacksDataRepeaterVirtualMode#2)]  
  
5.  分别为每个子控件的 <xref:System.Windows.Forms.Control.KeyDown> 事件实现一个处理程序并监视 Esc 键。  调用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A> 方法来防止引发 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> 事件。  代码与下面的示例类似。  
  
     [!CODE [VbPowerPacksDataRepeaterVirtualMode#3](../CodeSnippet/VS_Snippets_VBCSharp/VbPowerPacksDataRepeaterVirtualMode#3)]  
  
6.  为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded> 事件实现一个处理程序。  此事件在用户向 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中添加新项时引发。  代码与下面的示例类似，此示例针对一个名为 `Employees` 的数据源。  
  
     [!CODE [VbPowerPacksDataRepeaterVirtualMode#4](../CodeSnippet/VS_Snippets_VBCSharp/VbPowerPacksDataRepeaterVirtualMode#4)]  
  
7.  为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved> 事件实现一个处理程序。  此事件在用户删除现有项时发生。  代码与下面的示例类似，此示例针对一个名为 `Employees` 的数据源。  
  
     [!CODE [VbPowerPacksDataRepeaterVirtualMode#5](../CodeSnippet/VS_Snippets_VBCSharp/VbPowerPacksDataRepeaterVirtualMode#5)]  
  
8.  对于控件级验证，可选择为子控件的 <xref:System.Windows.Forms.Control.Validating> 事件实现处理程序。  代码与下面的示例类似。  
  
     [!CODE [VbPowerPacksDataRepeaterVirtualMode#6](../CodeSnippet/VS_Snippets_VBCSharp/VbPowerPacksDataRepeaterVirtualMode#6)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)