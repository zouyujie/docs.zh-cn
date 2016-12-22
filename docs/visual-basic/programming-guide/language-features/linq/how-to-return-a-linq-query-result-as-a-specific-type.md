---
title: "如何：以特定类型返回 LINQ 查询结果 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "匿名类型 [Visual Basic]"
  - "投影 [Visual Basic 中的 LINQ]"
  - "查询 [Visual Basic 中的 LINQ], 帮助主题"
  - "查询 [Visual Basic 中的 LINQ], 返回的特定类型"
  - "查询示例 [Visual Basic]"
  - "查询数据库 [LINQ]"
ms.assetid: 621bb10a-e5d7-44fb-a025-317964b19d92
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：以特定类型返回 LINQ 查询结果 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用语言集成查询 \(LINQ\) 可以方便地访问数据库信息和执行查询。  默认情况下，LINQ 查询以匿名类型返回对象列表。  使用 `Select` 子句，也可以指定查询返回特定类型的列表。  
  
 下面的示例演示如何创建对 SQL Server 数据库执行查询并将结果映射为特定命名类型的新应用程序。  有关更多信息，请参见[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)和 [Select 子句](../../../../visual-basic/language-reference/queries/select-clause.md)。  
  
 本主题中的示例使用 Northwind 示例数据库。  如果没有在开发计算机中安装 Northwind 示例数据库，可以从 [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088)（Microsoft 下载中心）网站下载该数据库。  有关说明，请参见[下载示例数据库](../Topic/Downloading%20Sample%20Databases.md)。  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
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
  
2.  单击 Customers 表并将它拖到设计器的左窗格上。  
  
     设计器为项目创建新的 `Customer` 对象。  可以将查询结果映射为 `Customer` 类型或您创建的类型。  此示例将在后面的过程中创建新类型并将查询结果映射为该类型。  
  
3.  保存所做的更改并关闭设计器。  
  
4.  保存您的项目。  
  
### 添加用于查询数据库和显示结果的代码  
  
1.  从**“工具箱”**中，将 <xref:System.Windows.Forms.DataGridView> 控件拖到项目的默认 Windows 窗体 Form1 上。  
  
2.  双击 Form1 以修改 Form1 类。  
  
3.  在 Form1 类的 `End Class` 语句后，添加下面的代码以创建 `CustomerInfo` 类型来保存此示例的查询结果。  
  
     [!CODE [VbLINQToSQLHowTos#16](../CodeSnippet/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos#16)]  
  
4.  将表添加到 O\/R 设计器后，设计器会向项目中添加一个 <xref:System.Data.Linq.DataContext> 对象。  此对象包含访问这些表以及访问每个表的单个对象和集合所必需的代码。  项目的 <xref:System.Data.Linq.DataContext> 对象是根据 .dbml 文件的名称命名的。  对于此项目，<xref:System.Data.Linq.DataContext> 对象被命名为 `northwindDataContext`。  
  
     可以在代码中创建 <xref:System.Data.Linq.DataContext> 的实例并查询通过 O\/R 设计器指定的表。  
  
     在 Form1 类的 `Load` 事件中，添加下面的代码来查询公开为数据上下文属性的表。  查询的 `Select` 子句将创建新的 `CustomerInfo` 类型，而不是为查询结果的每一项使用匿名类型。  
  
     [!CODE [VbLINQToSQLHowTos#15](../CodeSnippet/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos#15)]  
  
5.  按 F5 运行项目并查看结果。  
  
## 请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [DataContext 方法（O\/R 设计器）](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [演练：创建 LINQ to SQL 类（O\/R 设计器）](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)