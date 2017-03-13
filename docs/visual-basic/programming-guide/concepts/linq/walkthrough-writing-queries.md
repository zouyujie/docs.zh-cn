---
title: "演练：用 Visual Basic 编写查询 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "查询 [Visual Basic 中的 LINQ], 编写"
  - "LINQ [Visual Basic]，演练"
  - "LINQ [Visual Basic], 编写查询"
  - "编写 LINQ 查询 [Visual Basic]"
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
caps.latest.revision: 70
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 68
---
# 演练：用 Visual Basic 编写查询
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本演练演示了如何使用 Visual Basic 语言功能来编写 [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext-md.md)] 查询表达式。  本演练演示如何对一个 Student 对象列表创建查询、如何运行以及如何修改这些查询。  这些查询加入了 Visual Basic 2008 中的多项新功能，包括对象初始值设定项、局部类型推理和匿名类型。  
  
 完成本演练后，就可以转到所关注的特定 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序的示例和文档。  [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序包括 [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq-md.md)]、[!INCLUDE[linq_dataset](../../../../csharp/programming-guide/linq-query-expressions/includes/linq-dataset-md.md)] 和 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)]。  
  
## 创建项目  
  
#### 创建控制台应用程序项目  
  
1.  启动 Visual Studio。  
  
2.  在**“文件”**菜单上指向**“新建”**，再单击**“项目”**。  
  
3.  在**“已安装的模板”**列表中，单击**“Visual Basic”**。  
  
4.  在应用程序类型列表中，单击**“控制台应用程序”**。  在**“名称”**框中键入项目的名称，然后单击**“确定”**。  
  
     随即创建一个项目。  默认情况下，此项目包含对 System.Core.dll 的引用。  此外，[项目设计器 \-\>“引用”页 \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic) 上的**“导入的命名空间”**列表中还包括 <xref:System.Linq?displayProperty=fullName> 命名空间。  
  
5.  在 [“编译”页, 项目设计器 \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)，请确保 **option infer** 设置为。  
  
## 添加内存中数据源  
 本演练中查询的数据源是 `Student` 对象列表。  每个 `Student` 对象都包含名、姓、年级和在全体学生中的学习名次。  
  
#### 添加数据源  
  
-   定义 `Student` 类，然后创建该类的实例列表。  
  
    > [!IMPORTANT]
    >  [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)中提供了定义 `Student` 类和创建演练示例所使用的列表所需的代码。  您可以复制这些代码并将其粘贴到您的项目中。  新代码用于替换在您创建项目时显示的代码。  
  
#### 在学生列表中添加新学生  
  
-   按照 `getStudents` 方法中的模式将 `Student` 类的另一个实例添加到列表中。  添加学生涉及到对象初始值设定项。  有关更多信息，请参见[对象初始值设定项：命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。  
  
## 创建查询  
 执行本节添加的查询时，将生成学习名次位于前十位的学生列表。  由于查询每次都选择整个 `Student` 对象，因此查询结果的类型是 `IEnumerable(Of Student)`。  但是，查询的类型通常不在查询定义中指定，  而是由编译器使用局部类型推理来确定。  有关更多信息，请参见[局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。  查询的范围变量 `currentStudent` 用作对源 \(`students`\) 中每个 `Student` 实例的引用，以提供对 `students` 中每个对象属性的访问。  
  
#### 创建简单查询  
  
1.  在项目的 `Main` 方法中找到带如下标记的位置：  
  
     [!code-vb[VbLINQWalkthrough#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_1.vb)]  
  
     将下面的代码复制并粘贴到此位置。  
  
     [!code-vb[VbLINQWalkthrough#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_2.vb)]  
  
2.  将鼠标指针停留在代码中的 `studentQuery` 上，以验证编译器指定的类型是否为 `IEnumerable(Of Student)`。  
  
## 运行查询  
 变量 `studentQuery` 包含查询的定义，而非运行查询的结果。  运行查询的典型机制是 `For Each` 循环。  通过循环迭代变量来访问返回序列中的每个元素。  有关查询执行的更多信息，请参见[编写第一个 LINQ 查询](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)。  
  
#### 运行查询  
  
1.  将下面的 `For Each` 循环添加到项目中的查询下面。  
  
     [!code-vb[VbLINQWalkthrough#3](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_3.vb)]  
  
2.  将鼠标指针停留在循环控制变量 `studentRecord` 上，以查看其数据类型。  `studentRecord` 类型被推断为 `Student`，因为 `studentQuery` 返回 `Student` 实例的集合。  
  
3.  按 CTRL\+F5 生成并运行该应用程序。  注意控制台窗口中的结果。  
  
## 修改查询  
 如果结果按指定顺序排列，则浏览查询结果会更容易。  您可以根据任何可用字段对返回的序列进行排序。  
  
#### 对结果进行排序  
  
1.  将下面的 `Order By` 子句添加到查询的 `Where` 语句和 `Select` 语句之间。  `Order By` 子句将根据每个学生的姓按从 A 到 Z 的字母顺序对结果进行排序。  
  
    ```  
    Order By currentStudent.Last Ascending   
    ```  
  
2.  若要先按姓再按名进行排序，请将两个字段都添加到查询：  
  
    ```  
    Order By currentStudent.Last Ascending, currentStudent.First Ascending   
    ```  
  
     您也可以指定 `Descending`，以便按从 Z 到 A 的顺序排序。  
  
3.  按 CTRL\+F5 生成并运行该应用程序。  注意控制台窗口中的结果。  
  
#### 引入本地标识符  
  
1.  添加本节中的代码，将本地标识符引入查询表达式。  该本地标识符将保存中间结果。  在下面的示例中，`name` 是保存学生姓和名的串联的标识符。  本地标识符可以提供方便，也可以通过存储表达式的结果来避免多次计算，从而提高性能。  
  
     [!code-vb[VbLINQWalkthrough#4](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_4.vb)]  
  
2.  按 CTRL\+F5 生成并运行该应用程序。  注意控制台窗口中的结果。  
  
#### 在 Select 子句中投影一个字段  
  
1.  添加本节中的查询和 `For Each` 循环以创建一个查询，该查询将生成一个其元素与源中元素不同的序列。  在下面的示例中，源是 `Student` 对象的集合，但是只返回每个对象的一个成员：姓氏为 Garcia 的学生的名字。  由于 `currentStudent.First` 是一个字符串，因此 `studentQuery3` 返回的序列的数据类型是 `IEnumerable(Of String)`，为字符串序列。  如前面的示例所示，`studentQuery3` 数据类型的分配由编译器使用局部类型推理来确定。  
  
     [!code-vb[VbLINQWalkthrough#5](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_5.vb)]  
  
2.  将鼠标指针停留在代码中的 `studentQuery3` 上，以验证分配的类型是否为 `IEnumerable(Of String)`。  
  
3.  按 CTRL\+F5 生成并运行该应用程序。  注意控制台窗口中的结果。  
  
#### 在 Select 子句中创建匿名类型  
  
1.  添加本节中的代码以了解在查询中如何使用匿名类型。  当您希望从数据源返回多个字段而不是返回完整记录（前面示例中的 `currentStudent` 记录）或单个字段（前一节中的 `First`）时，可以在查询中使用匿名类型。  而不是定义包含字段要包含在结果中的新命名类型，可以在 `Select` 子句指定字段，并且编译器使用这些字段创建匿名类型作为其属性。有关更多信息，请参见[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
     下面的示例创建一个查询，返回学习名次位于 1 和 10 之间的高年级学生的姓名和学习名次，并按学习名次排序。  在本例中，必须推断 `studentQuery4` 的类型，因为 `Select` 子句返回匿名类型的实例，而匿名类型没有可用的名称。  
  
     [!code-vb[VbLINQWalkthrough#6](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_6.vb)]  
  
2.  按 CTRL\+F5 生成并运行该应用程序。  注意控制台窗口中的结果。  
  
## 其他示例  
 现在您已经了解了基础知识，接下来是一组演示 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询的灵活性和强大功能的其他示例。  每个示例之前有描述其用途的简要说明。  停留在查询结果变量的鼠标指针每个查询的查看推断的类型。使用一个 `For Each` 循环生成结果。  
  
 [!code-vb[VbLINQWalkthrough#7](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_7.vb)]  
  
## 其他信息  
 熟悉使用查询的基本概念之后，就可以开始阅读所关注的特定类型的 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序的文档和示例：  
  
 [LINQ to Objects](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)  
  
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)  
  
 [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)  
  
 [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md)  
  
## 请参阅  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Getting Started with LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Supplementary LINQ Resources](../Topic/Supplementary%20LINQ%20Resources.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [对象初始值设定项：命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [Walkthrough: Writing Queries in C\#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)