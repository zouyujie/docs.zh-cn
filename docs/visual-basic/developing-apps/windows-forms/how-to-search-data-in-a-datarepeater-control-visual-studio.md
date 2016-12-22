---
title: "如何：在 DataRepeater 控件中搜索数据 (Visual Studio) | Microsoft Docs"
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
  - "DataRepeater, 实现搜索"
  - "DataRepeater, 搜索数据"
ms.assetid: a8ab5d17-b94f-43c4-8dd7-d0450226d73f
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 DataRepeater 控件中搜索数据 (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

当使用包含大量记录的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件时，您可能会希望允许用户搜索特定的记录。  与在控件自身中搜索数据不同，您可以通过查询底层的 <xref:System.Windows.Forms.BindingSource> 来实现搜索。  如果找到了项，便可以使用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndex%2A> 属性来选择该项并将它滚动到视图中。  
  
### 实现搜索  
  
1.  从**“工具箱”**中将 <xref:System.Windows.Forms.TextBox> 控件拖到包含 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的窗体中。  
  
2.  在“属性”窗口中，将**“Name”**属性更改为 SearchTextBox。  
  
3.  从**“工具箱”**中将 <xref:System.Windows.Forms.Button> 控件拖到包含 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的窗体中。  
  
4.  在“属性”窗口中，将**“Name”**属性更改为 SearchButton。  将**“Text”**属性更改为 Search。  
  
5.  双击 <xref:System.Windows.Forms.Button> 控件打开代码编辑器，并将下面的代码添加到 `SearchButton_Click` 事件处理程序中。  
  
     [!CODE [VbPowerPacksDataRepeaterSearch#1](../CodeSnippet/VS_Snippets_VBCSharp/VbPowerPacksDataRepeaterSearch#1)]  
  
     将 *ProductsBindingSource* 替换为您的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 的 <xref:System.Windows.Forms.BindingSource> 的名称，并将 *ProductID* 替换为要搜索的字段的名称。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [如何：更改 DataRepeater 控件的外观](../Topic/How%20to:%20Change%20the%20Appearance%20of%20a%20DataRepeater%20Control%20\(Visual%20Studio\).md)