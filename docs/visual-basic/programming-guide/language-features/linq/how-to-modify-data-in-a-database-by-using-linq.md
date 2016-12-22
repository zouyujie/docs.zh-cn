---
title: "如何：使用 LINQ 修改数据库中的数据 (Visual Basic) | Microsoft Docs"
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
  - "数据 [Visual Basic], 更新"
  - "删除数据"
  - "删除行 [LINQ to SQL]"
  - "插入数据 [Visual Basic]"
  - "插入行 [LINQ to SQL]"
  - "查询 [Visual Basic 中的 LINQ], 数据库中的数据更改"
  - "查询 [Visual Basic 中的 LINQ], 帮助主题"
  - "更新数据 [LINQ]"
  - "更新行 [LINQ to SQL]"
ms.assetid: cf52635f-0c1b-46c3-aff1-bdf181cf19b1
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：使用 LINQ 修改数据库中的数据 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用语言集成查询 \(LINQ\) 可以方便地访问数据库信息和修改数据库中的值。  
  
 下面的示例演示如何创建用于检索和更新 SQL Server 数据库信息的新应用程序。  
  
 本主题中的示例使用 Northwind 示例数据库。  如果没有在开发计算机中安装 Northwind 示例数据库，可以从 [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088)（Microsoft 下载中心）网站下载该数据库。  有关说明，请参见[下载示例数据库](../Topic/Downloading%20Sample%20Databases.md)。  
  
### 创建与数据库的连接  
  
1.  在 Visual Studio 中，单击**“视图”**菜单，选择**“服务器资源管理器”**\/**“数据库资源管理器”**，打开**“服务器资源管理器”**\/**“数据库资源管理器”**。  
  
2.  在**“服务器资源管理器”**\/**“数据库资源管理器”**中，右击**“数据连接”**，然后单击**“添加连接”**。  
  
3.  指定与 Northwind 示例数据库的有效连接。  
  
### 将 LINQ to SQL 文件添加到项目  
  
1.  在 Visual Studio 中的**“文件”**菜单上，指向**“新建”**，然后单击**“项目”**。  选择 Visual Basic**“Windows 窗体应用程序”**作为项目类型。  
  
2.  在**“项目”**菜单上，单击**“添加新项”**。  选择**“LINQ to SQL 类”**项模板。  
  
3.  将文件命名为 `northwind.dbml`。  单击**“添加”**。  为 `northwind.dbml` 文件打开对象关系设计器（O\/R 设计器）。  
  
### 将要查询和修改的表添加到设计器  
  
1.  在**“服务器资源管理器”**\/**“数据库资源管理器”**中，展开与 Northwind 数据库的连接。  展开**“表”**文件夹。  
  
     如果已经关闭 O\/R 设计器，可以通过双击先前添加的 `northwind.dbml` 文件重新将其打开。  
  
2.  单击 Customers 表并将它拖到设计器的左窗格上。  
  
     设计器为项目创建新的 Customer 对象。  
  
3.  保存所做的更改并关闭设计器。  
  
4.  保存您的项目。  
  
### 添加用于修改数据库和显示结果的代码  
  
1.  从**“工具箱”**中，将 <xref:System.Windows.Forms.DataGridView> 控件拖到项目的默认 Windows 窗体 Form1 上。  
  
2.  将表添加到 O\/R 设计器后，设计器会向项目中添加一个 <xref:System.Data.Linq.DataContext> 对象。  此对象包含可用于访问 Customers 表的代码。  还包含为表定义局部 Customer 对象和 Customers 集合的代码。  项目的 <xref:System.Data.Linq.DataContext> 对象是根据 .dbml 文件的名称命名的。  对于此项目，<xref:System.Data.Linq.DataContext> 对象被命名为 `northwindDataContext`。  
  
     可以在代码中创建 <xref:System.Data.Linq.DataContext> 对象的实例，也可以查询和修改 O\/R 设计器所指定的 Customers 集合。  通过调用 <xref:System.Data.Linq.DataContext> 对象的 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 方法提交对 Customers 集合所做的更改之后，这些更改才会在数据库中反映出来。  
  
     双击 Windows 窗体 Form1，可将代码添加到 <xref:System.Windows.Forms.Form.Load> 事件，以便查询公开为 <xref:System.Data.Linq.DataContext> 的属性的 Customers 表。  添加下列代码：  
  
    ```vb#  
    Private db As northwindDataContext  
  
    Private Sub Form1_Load(ByVal sender As System.Object,   
                           ByVal e As System.EventArgs  
                          ) Handles MyBase.Load  
      db = New northwindDataContext()  
  
      RefreshData()  
    End Sub  
  
    Private Sub RefreshData()  
      Dim customers = From cust In db.Customers   
                      Where cust.City(0) = "W"   
                      Select cust  
  
      DataGridView1.DataSource = customers  
    End Sub  
    ```  
  
3.  从**“工具箱”**中将三个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  选择第一个 `Button` 控件。  在**“属性”**窗口中，将 `Button` 控件的 `Name` 设置为 `AddButton`，将 `Text` 设置为 `Add`。  选择第二个按钮，将 `Name` 属性设置为 `UpdateButton`，将 `Text` 属性设置为 `Update`。  选择第三个按钮，将 `Name` 属性设置为 `DeleteButton`，将 `Text` 属性设置为 `Delete`。  
  
4.  双击**“Add”**按钮，向其 `Click` 事件添加代码。  添加下列代码：  
  
    ```vb#  
    Private Sub AddButton_Click(ByVal sender As System.Object,   
                                ByVal e As System.EventArgs  
                               ) Handles AddButton.Click  
      Dim cust As New Customer With {   
        .City = "Wellington",   
        .CompanyName = "Blue Yonder Airlines",   
        .ContactName = "Jill Frank",   
        .Country = "New Zealand",   
        .CustomerID = "JILLF"}  
  
      db.Customers.InsertOnSubmit(cust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
5.  双击**“Update”**按钮，向其 `Click` 事件添加代码。  添加下列代码：  
  
    ```vb#  
    Private Sub UpdateButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles UpdateButton.Click  
      Dim updateCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      updateCust.ContactName = "Jill Shrader"  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
6.  双击**“Delete”**按钮，向其 `Click` 事件添加代码。  添加下列代码：  
  
    ```vb#  
    Private Sub DeleteButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles DeleteButton.Click  
      Dim deleteCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      db.Customers.DeleteOnSubmit(deleteCust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
7.  按 F5 运行项目。  单击**“Add”**添加新记录。  单击**“Update”**修改该新记录。  单击**“Delete”**删除该新记录。  
  
## 请参阅  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [DataContext 方法（O\/R 设计器）](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [如何：分配存储过程以执行更新、插入和删除（O\/R 设计器）](../Topic/How%20to:%20Assign%20stored%20procedures%20to%20perform%20updates,%20inserts,%20and%20deletes%20\(O-R%20Designer\).md)   
 [演练：创建 LINQ to SQL 类（O\/R 设计器）](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)