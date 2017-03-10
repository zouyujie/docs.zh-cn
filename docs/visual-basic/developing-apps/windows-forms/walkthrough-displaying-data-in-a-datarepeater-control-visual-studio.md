---
title: "演练：在 DataRepeater 控件中显示数据 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 演练"
ms.assetid: 65dcdb95-6c3e-47cc-987d-190000f71653
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 演练：在 DataRepeater 控件中显示数据 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

本演练提供了在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中显示绑定数据的完整基本方案。  
  
## 必备组件  
 本演练需要 Northwind 示例数据库。  
  
 如果你的开发计算机上没有此数据库，可以从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=98088)进行下载。 有关说明，请参阅[下载示例数据库](../Topic/Downloading%20Sample%20Databases.md)。  
  
## 概述  
 本演练的第一部分主要有以下四个任务：  
  
-   创建解决方案。  
  
-   添加 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件。  
  
-   添加数据源。  
  
-   添加数据绑定控件。  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
## 创建 DataRepeater 解决方案  
 在第一步中，创建项目和解决方案。  
  
#### 创建 DataRepeater 解决方案的步骤  
  
1.  在 Visual Studio“文件”菜单上，单击“新建项目”。  
  
2.  在**“新建项目”**对话框中的**“项目类型”**窗格中，展开**“Visual Basic”**，然后单击**“Windows”**。  
  
3.  在**“模板”**窗格中，单击**“Windows 窗体应用程序”**。  
  
4.  在“名称”框中键入 `DataRepeaterApp`。  
  
5.  单击“确定”。  
  
     Windows 窗体设计器即会打开。  
  
6.  在“Windows 窗体设计器”中选择窗体。 在“属性”窗口中，将“Size”属性设置为 `800, 700`。  
  
## 添加 DataRepeater 控件  
 在此步骤中，向窗体添加一个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件。  
  
#### 添加 DataRepeater 控件的步骤  
  
1.  在**“视图”**菜单上单击**“工具箱”**。  
  
     将打开**“工具箱”**。  
  
2.  选择“Visual Basic PowerPacks”选项卡。  
  
3.  将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件拖到“Form1”上。  
  
4.  在“属性”窗口中，将“Location”属性设置为 `0, 25`。  
  
5.  将“Size”属性设置为 `460, 600`。  
  
## 添加数据源  
 在此步骤中，为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件添加一个数据源。  
  
#### 添加数据源  
  
1.  在**“数据”**菜单上，单击**“显示数据源”**。  
  
2.  在**“数据源”**窗口中，单击**“添加新数据源”**。  
  
3.  在**“选择数据源类型”**页上选择**“数据库”**，然后单击**“下一步”**。  
  
4.  在**“选择你的数据连接”**页上执行下列步骤之一：  
  
    -   如果下拉列表中包含到 Northwind 示例数据库的数据连接，请单击该连接。  
  
         \- 或 \-  
  
    -   单击“新建连接”来配置新数据连接。 有关详细信息，请参阅[How to: Create Connections to SQL Server Databases](http://msdn.microsoft.com/zh-cn/360c340d-e5a6-4a7e-a569-e95d500be43d)。  
  
5.  如果数据库需要密码，请选择该选项以包括敏感数据，然后单击**“下一步”**。  
  
    > [!NOTE]
    >  如果显示一个对话框，请单击“是”将该文件保存到你的项目中。  
  
6.  在“将连接字符串保存到应用程序配置文件”页面上单击“下一步”。  
  
7.  在**“选择数据库对象”**页面上展开**“表”**节点。  
  
8.  选中“Customers”和“Orders”表旁边的复选框，然后单击“完成”。  
  
     “NorthwindDataSet”将会添加到你的项目中，并且在“数据源”窗口中将显示“Customers”和“Orders”表。  
  
## 添加数据绑定控件  
 在此步骤中，向 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 添加数据绑定控件。  
  
#### 添加数据绑定控件  
  
1.  在“数据源”窗口中，选择“Customers”表的顶级节点。  
  
2.  通过在表节点上的下拉列表中单击“详细信息”，将该表的拖放类型更改为“详细信息”。  
  
3.  选择“Customers”表节点，将它拖到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板区域（上半部分区域）。  
  
     一个 <xref:System.Windows.Forms.BindingNavigator> 控件添加到窗体中，并且“NorthwindDataSet”、“CustomersBindingSource”、“CustomersTableAdapter”、“TableAdapterManager”和“CustomersBindingNavigator”组件添加到组件栏中。  
  
4.  选择所有字段及其关联标签，并将它们置于项模板区域左边缘附近。  
  
5.  选择后五个字段（“Region”、“Postal Code”、“Country”、“Phone”和“Fax”）及其关联标签，并将它们上移到前六个字段的右侧。  
  
6.  选择项模板（控件的上半部分区域）。  
  
7.  在“属性”窗口中，将“Size”属性设置为 `427, 170`。  
  
 此时，你就得到了一个有效的应用程序，该应用程序将显示客户的重复列表。 可以按 F5 运行该应用程序、更改数据以及添加或删除客户记录。  
  
 在后续的可选步骤中，你将学习如何自定义 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件。  
  
## 后续步骤（可选）  
 演练的本部分有以下四个可选任务：  
  
-   更改 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的外观。  
  
-   防止用户添加或删除记录。  
  
-   向 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件添加搜索功能。  
  
-   向 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件添加主表和详细信息表。  
  
## 更改 DataRepeater 控件的外观  
 在此可选步骤中，你将在设计时更改 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的 `BackColor`。 你还将添加代码来以交替颜色显示行以及有条件地更改标签的 `ForeColor`。  
  
#### 更改控件外观的步骤  
  
1.  在 Windows 窗体设计器中，选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的主（下半部分）区域。  
  
2.  在“属性”窗口中，将 `BackColor` 属性设置为白色。  
  
3.  双击 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 打开代码编辑器。  
  
4.  在代码编辑器中，在“事件”下拉列表中单击“DrawItem”。  
  
5.  在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件处理程序中添加下面的代码为 `BackColor` 提供一个交替值：  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DataRepeaterAppCS/DataRepeaterWalkthrough.cs#1)]
     [!code-vb[VbPowerPacksDataRepeaterWalkthrough#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/DataRepeaterApp/DataRepeaterWalkthrough.vb#1)]  
  
6.  在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件处理程序中添加下面的代码，以根据条件更改某个标签的 `ForeColor`：  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DataRepeaterAppCS/DataRepeaterWalkthrough.cs#2)]
     [!code-vb[VbPowerPacksDataRepeaterWalkthrough#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/DataRepeaterApp/DataRepeaterWalkthrough.vb#2)]  
  
7.  按 F5 运行该应用程序并查看自定义项。  
  
## 防止用户添加或删除记录  
 在此可选步骤中，你将添加代码来防止用户在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中添加或删除记录。  
  
#### 防止用户添加和删除记录的步骤  
  
1.  在 Windows 窗体设计器中，双击窗体打开代码编辑器。  
  
2.  将以下代码添加到 `Form_Load` 事件中：  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough#3](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DataRepeaterAppCS/DataRepeaterWalkthrough.cs#3)]
     [!code-vb[VbPowerPacksDataRepeaterWalkthrough#3](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/DataRepeaterApp/DataRepeaterWalkthrough.vb#3)]  
  
3.  在“类名”下拉列表中单击“BindingNavigatorDeleteItem”。 在“方法名称”下拉列表中单击“EnabledChanged”。  
  
4.  将以下代码添加到 `BindingNavigatorDeleteItem_EnabledChanged` 事件处理程序中：  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough#4](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DataRepeaterAppCS/DataRepeaterWalkthrough.cs#4)]
     [!code-vb[VbPowerPacksDataRepeaterWalkthrough#4](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/DataRepeaterApp/DataRepeaterWalkthrough.vb#4)]  
  
    > [!NOTE]
    >  此步骤是必需的，因为每当当前记录发生更改时，<xref:System.Windows.Forms.BindingSource> 都将启用“删除项”按钮。  
  
5.  按 F5 运行该应用程序。 请注意，“删除项”按钮处于禁用状态，你无法通过按 Delete 键来删除项。  
  
## 向 DataRepeater 控件添加搜索功能  
 在此可选步骤中，你将实现在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中搜索值的功能。 如果找到了搜索字符串，该控件将选中包含该值的项并将该项滚动到视图中。  
  
#### 添加搜索功能的步骤  
  
1.  从“工具箱”中将 <xref:System.Windows.Forms.TextBox> 控件拖到包含 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的窗体上。  
  
     将它置于 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的下方。  
  
2.  在“属性”窗口中，将“Name”属性更改为 **SearchTextBox**。  
  
3.  从“工具箱”中将 <xref:System.Windows.Forms.Button> 控件拖到包含 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的窗体上。 将它置于 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的下方。  
  
4.  在“属性”窗口中，将“Name”属性更改为 **SearchButton**。 将“Text”属性更改为 **Search**。  
  
5.  双击 <xref:System.Windows.Forms.Button> 控件打开代码编辑器，并将以下代码添加到 `SearchButton_Click` 事件处理程序中。  
  
     [!code-cs[VbPowerPacksDataRepeaterWalkthrough#5](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DataRepeaterAppCS/DataRepeaterWalkthrough.cs#5)]
     [!code-vb[VbPowerPacksDataRepeaterWalkthrough#5](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/DataRepeaterApp/DataRepeaterWalkthrough.vb#5)]  
  
6.  按 F5 运行该应用程序。 在“搜索文本框”中键入一个客户 ID 并单击“搜索”按钮。  
  
## 向 DataRepeater 添加主表和详细信息表  
 在此可选步骤中，你将再添加一个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件来显示每个客户的相关订单。  
  
#### 添加主表和详细信息表的步骤  
  
1.  从“工具箱”的“Visual Basic PowerPacks”选项卡中再将一个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件拖到窗体上。  
  
2.  在“属性”窗口中，将“Location”属性设置为 `465, 25`。  
  
3.  将“Size”属性设置为 `315, 600`。  
  
4.  在“数据源”窗口中，展开“Customers”表节点，然后选择“Orders”表的详细信息节点。  
  
5.  通过在表节点上的下拉列表中单击“详细信息”，将该“Orders”表的拖放类型更改为“详细信息”。  
  
6.  将该“Orders”表节点拖到第二个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板区域（上半部分区域）。  
  
     “OrdersBindingSource”组件和“OrdersTableAdapter”组件即添加到组件栏中。  
  
7.  按 F5 运行该应用程序。 当你在第一个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中选择每个客户时，该客户的订单会显示在第二个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中。  
  
## 请参阅  
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示未绑定的控件](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [如何：更改 DataRepeater 控件的布局](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示项标题](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中搜索数据](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md)   
 [如何：使用两个 DataRepeater 控件创建主\/详细信息窗体](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [如何：更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [如何：禁止添加和删除 DataRepeater 项](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)