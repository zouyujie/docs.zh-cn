---
title: "如何：使用 LINQ 调用存储过程 (Visual Basic) | Microsoft Docs"
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
  - "查询 [Visual Basic 中的 LINQ], 帮助主题"
  - "查询 [Visual Basic 中的 LINQ], 存储过程调用"
  - "存储过程 [LINQ to SQL]"
  - "存储过程示例 [Visual Basic]"
ms.assetid: 6436d384-d1e0-40aa-8afd-451007477260
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：使用 LINQ 调用存储过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用语言集成查询 \(LINQ\) 可以方便地访问数据库信息（包括存储过程等数据库对象）。  
  
 下面的示例演示如何创建调用 SQL Server 数据库中的存储过程的应用程序。  该示例演示如何调用数据库中的两个不同的存储过程。  每个过程都返回查询结果。  一个过程采用输入参数，另一个过程不采用参数。  
  
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
  
### 将存储过程添加到 O\/R 设计器上  
  
1.  在**“服务器资源管理器”**\/**“数据库资源管理器”**中，展开与 Northwind 数据库的连接。  展开**“存储过程”**文件夹。  
  
     如果已经关闭 O\/R 设计器，可以通过双击先前添加的 northwind.dbml 文件重新将其打开。  
  
2.  单击**“Sales by Year”**存储过程并将它拖到设计器的右窗格中。  单击**“Ten Most Expensive Products”**存储过程并将它拖到设计器的右窗格中。  
  
3.  保存所做的更改并关闭设计器。  
  
4.  保存您的项目。  
  
### 添加用于显示存储过程结果的代码  
  
1.  从**“工具箱”**中，将 <xref:System.Windows.Forms.DataGridView> 控件拖到项目的默认 Windows 窗体 Form1 上。  
  
2.  双击 Form1，向其 `Load` 事件添加代码。  
  
3.  将存储过程添加到 O\/R 设计器后，设计器会为项目添加一个 <xref:System.Data.Linq.DataContext> 对象。  此对象包含访问这些过程所必需的代码。  项目的 <xref:System.Data.Linq.DataContext> 对象是根据 .dbml 文件的名称命名的。  对于此项目，<xref:System.Data.Linq.DataContext> 对象被命名为 `northwindDataContext`。  
  
     可以在代码中创建 <xref:System.Data.Linq.DataContext> 的实例并调用 O\/R 设计器指定的存储过程方法。  若要绑定到 <xref:System.Windows.Forms.DataGridView> 对象，必须强制查询通过对存储过程的结果调用 <xref:System.Linq.Enumerable.ToList%2A> 方法立即执行。  
  
     将下面的代码添加到 `Load` 事件，以调用任一公开为数据上下文的方法的存储过程。  
  
     [!CODE [VbLINQtoSQLHowTos#1](../CodeSnippet/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos#1)]  
    [!CODE [VbLINQtoSQLHowTos#2](../CodeSnippet/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos#2)]  
  
4.  按 F5 运行项目并查看结果。  
  
## 请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [DataContext 方法（O\/R 设计器）](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [如何：分配存储过程以执行更新、插入和删除（O\/R 设计器）](../Topic/How%20to:%20Assign%20stored%20procedures%20to%20perform%20updates,%20inserts,%20and%20deletes%20\(O-R%20Designer\).md)   
 [演练：创建 LINQ to SQL 类（O\/R 设计器）](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)