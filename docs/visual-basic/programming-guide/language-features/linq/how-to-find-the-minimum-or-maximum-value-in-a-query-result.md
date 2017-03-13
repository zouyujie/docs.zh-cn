---
title: "如何：使用 LINQ 查找查询结果中的最小值或最大值 (Visual Basic) | Microsoft Docs"
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
  - "Aggregate 子句"
  - "聚合运算符 [Visual Basic 中的 LINQ]"
  - "聚合查询"
  - "最大值运算符 [Visual Basic 中的 LINQ]"
  - "Max 属性"
  - "最大值 [Visual Basic 中的 LINQ]"
  - "最小值运算符 [Visual Basic 中的 LINQ]"
  - "最小值 [Visual Basic 中的 LINQ]"
  - "查询 [Visual Basic 中的 LINQ], 聚合查询"
  - "查询 [Visual Basic 中的 LINQ], 帮助主题"
  - "查询 [Visual Basic 中的 LINQ], 最小值和最大值"
ms.assetid: 238b763b-7dcd-4b14-8050-b65500a4f71c
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 如何：使用 LINQ 查找查询结果中的最小值或最大值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用语言集成查询 \(LINQ\) 可以方便地访问数据库信息和执行查询。  
  
 下面的示例演示如何创建对 SQL Server 数据库执行查询的新应用程序。  该示例使用 `Aggregate` 和 `Group By` 子句确定结果的最小值和最大值。  有关更多信息，请参见 [Aggregate 子句](../../../../visual-basic/language-reference/queries/aggregate-clause.md) 和 [Group By 子句](../../../../visual-basic/language-reference/queries/group-by-clause.md)。  
  
 本主题中的示例使用 Northwind 示例数据库。  如果没有在开发计算机中安装 Northwind 示例数据库，可以从 [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088)（Microsoft 下载中心）网站下载该数据库。  有关说明，请参见[下载示例数据库](../Topic/Downloading%20Sample%20Databases.md)。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### 创建与数据库的连接  
  
1.  在 Visual Studio 中，通过在**“视图”**菜单上单击**“服务器资源管理器”**\/**“数据库资源管理器”**，打开**“服务器资源管理器”**\/**“数据库资源管理器”**。  
  
2.  在**“服务器资源管理器”**\/**“数据库资源管理器”**中，右击**“数据连接”**，然后单击**“添加连接”**。  
  
3.  指定与 Northwind 示例数据库的有效连接。  
  
### 添加包含 LINQ to SQL 文件的项目  
  
1.  在 Visual Studio 中的**“文件”**菜单上，指向**“新建”**，然后单击**“项目”**。  选择 Visual Basic**“Windows 窗体应用程序”**作为项目类型。  
  
2.  在**“项目”**菜单上，单击**“添加新项”**。  选择**“LINQ to SQL 类”**项模板。  
  
3.  将文件命名为 `northwind.dbml`。  单击**“添加”**。  为 northwind.dbml 文件打开对象关系设计器（O\/R 设计器）。  
  
### 将要查询的表添加到 O\/R 设计器  
  
1.  在**“服务器资源管理器”**\/**“数据库资源管理器”**中，展开与 Northwind 数据库的连接。  展开**“表”**文件夹。  
  
     如果已经关闭 O\/R 设计器，可以通过双击先前添加的 northwind.dbml 文件重新将其打开。  
  
2.  单击 Customers 表并将它拖到设计器的左窗格上。  单击 Orders 表并将它拖到设计器的左窗格上。  
  
     设计器为项目创建新的 `Customer` 和 `Order` 对象。  请注意，设计器会自动检测表之间的关系并为相关对象创建子属性。  例如，IntelliSense 会显示 `Customer` 对象具有一个 `Orders` 属性，该属性对应于所有与该客户相关的订单。  
  
3.  保存所做的更改并关闭设计器。  
  
4.  保存您的项目。  
  
### 添加用于查询数据库和显示结果的代码  
  
1.  从**“工具箱”**中，将 <xref:System.Windows.Forms.DataGridView> 控件拖到项目的默认 Windows 窗体 Form1 上。  
  
2.  双击 Form1，以便将代码添加到该窗体的 `Load` 事件。  
  
3.  将表添加到 O\/R 设计器后，设计器会为项目添加一个 <xref:System.Data.Linq.DataContext> 对象。  此对象包含访问这些表以及访问每个表的各个对象和集合所必需的代码。  项目的 <xref:System.Data.Linq.DataContext> 对象是根据 .dbml 文件的名称命名的。  对于此项目，<xref:System.Data.Linq.DataContext> 对象被命名为 `northwindDataContext`。  
  
     可以在代码中创建 <xref:System.Data.Linq.DataContext> 的实例并查询通过 O\/R 设计器指定的表。  
  
     将下面的代码添加到 `Load` 事件中。  这段代码查询作为数据上下文的属性公开的表，并确定结果的最小值和最大值。  该示例使用 `Aggregate` 子句查询单个结果，使用 `Group By` 子句显示分组结果的平均值。  
  
     [!code-vb[VbLINQToSQLHowTos#14](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-find-the-minimum-or-maximum-value-in-a-query-result_1.vb)]  
  
4.  按 F5 运行项目并查看结果。  
  
## 请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [DataContext 方法（O\/R 设计器）](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [演练：创建 LINQ to SQL 类（O\/R 设计器）](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)