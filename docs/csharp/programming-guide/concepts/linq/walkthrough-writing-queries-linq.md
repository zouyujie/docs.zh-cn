---
title: "Walkthrough: Writing Queries in C# (LINQ) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.topic: "get-started-article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "LINQ [C#], walkthroughs"
  - "LINQ [C#], writing queries"
  - "queries [LINQ in C#], writing"
  - "writing LINQ queries"
ms.assetid: 2962a610-419a-4276-9ec8-4b7f2af0c081
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# Walkthrough: Writing Queries in C# (LINQ)
本演练演示了用于编写 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 查询表达式的 C\# 语言功能。  完成本演练后，您便可以继续学习您感兴趣的具体 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序（如 [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq-md.md)]、[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] to DataSet 或 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)]）的示例和文档。  
  
## 系统必备  
 本演练需要在 Visual Studio 2008 中引入\) 的功能。  
  
 ![链接到视频](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") 有关该主题的视频版本，请参见 [Video How to: Writing Queries in C\# \(LINQ\)](http://go.microsoft.com/fwlink/?LinkId=100393)（视频帮助主题：在 C\# 中编写查询 \(LINQ\)）。  
  
## 创建 C\# 项目  
  
#### 创建项目  
  
1.  启动 Visual Studio。  
  
2.  在菜单栏上，选择**“文件”**，**“新建**、**“项目”**。  
  
     将打开**“新建项目”**对话框。  
  
3.  外接 **已安装**，展开 **模板**，展开 **Visual C\#**，然后选择 **控制台应用程序**。  
  
4.  在 **名称** 文本框中，输入一个不同的名称或接受默认名称，然后选择 **确定** 按钮。  
  
     新项目出现在**“解决方案资源管理器”**中。  
  
5.  请注意，您的项目具有对 System.Core.dll 的引用以及适用于 <xref:System.Linq?displayProperty=fullName> 命名空间的 `using` 指令。  
  
## 创建内存中数据源  
 查询的数据源是 `Student` 对象的简单列表。  每个 `Student` 记录都有名、姓和表示他们在班级中的测验分数的整数数组。  将此代码复制到您的项目。  请注意下列特性：  
  
-   `Student` 类包含自动实现的属性。  
  
-   列表中的每个学生都已使用对象初始值设定项进行初始化。  
  
-   列表本身已使用集合初始值设定项进行初始化。  
  
 将在不显式调用任何构造函数和使用显式成员访问的情况下初始化并实例化整个数据结构。  有关这些新功能的更多信息，请参见[自动实现的属性](../../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)和[对象和集合初始值设定项](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)。  
  
#### 添加数据源  
  
-   将 `Student` 类和经过初始化的学生列表添加到您的项目的 `Program` 类中。  
  
     [!code-cs[CsLinqGettingStarted#11](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_1.cs)]  
  
#### 在学生列表中添加新学生  
  
1.  将新 `Student` 添加到 `Students` 列表中并使用您选择的姓名和测验分数。  尝试键入新学生的所有信息，以便更好地了解对象初始值设定项的语法。  
  
## 创建查询  
  
#### 创建简单查询  
  
-   在应用程序的 `Main` 方法中创建一个简单查询，执行该查询时，将生成第一次测验中分数高于 90 分的所有学生的列表。  请注意，由于选择了整个 `Student` 对象，因此查询的类型是 `IEnumerable<Student>`。  虽然代码也可以通过使用 [var](../../../../csharp/language-reference/keywords/var.md) 关键字来使用隐式类型，但这里使用了显式类型以便清楚地演示结果。  （有关 `var` 的更多信息，请参见[隐式类型的局部变量](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。）  
  
     另请注意，该查询的范围变量 `student` 用作对源中每个 `Student` 的引用，以提供对每个对象的成员访问。  
  
 [!code-cs[CsLINQGettingStarted#12](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_2.cs)]  
  
## 执行查询  
  
#### 执行查询  
  
1.  现在编写用于执行查询的 `foreach` 循环。  请注意有关代码的以下事项：  
  
    -   所返回序列中的每个元素是通过 `foreach` 循环中的迭代变量来访问的。  
  
    -   此变量的类型是 `Student`，查询变量的类型是兼容的 `IEnumerable<Student>`。  
  
2.  添加此代码后，按 Ctrl \+ F5 生成并运行该应用程序，然后在**“控制台”**窗口中查看结果。  
  
 [!code-cs[CsLINQGettingStarted#13](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_3.cs)]  
  
#### 添加另一个筛选条件  
  
1.  您可以在 `where` 子句中组合多个布尔条件，以便进一步细化查询。  下面的代码添加一个条件，以便查询返回第一个分数高于 90 分并且最后一个分数低于 80 分的那些学生。  `where` 子句应类似于以下代码。  
  
    ```  
    where student.Scores[0] > 90 && student.Scores[3] < 80  
    ```  
  
     有关更多信息，请参见[where 子句](../../../../csharp/language-reference/keywords/where-clause.md)。  
  
## 修改查询  
  
#### 对结果进行排序  
  
1.  如果结果按某种顺序排列，则浏览结果会更容易。  您可以根据源元素中的任何可访问字段对返回的序列进行排序。  例如，下面的 `orderby` 子句根据每个学生的姓按从 A 到 Z 的字母顺序对结果进行排序。  紧靠在 `where` 语句之后、`select` 语句之前，将下面的 `orderby` 子句添加到您的查询中：  
  
    ```  
    orderby student.Last ascending  
    ```  
  
2.  现在更改 `orderby` 子句，以便根据第一次测验的分数的反向顺序，即从高分到低分的顺序对结果进行排序。  
  
    ```  
    orderby student.Scores[0] descending  
    ```  
  
3.  更改 `WriteLine` 格式字符串以便您可以查看分数：  
  
    ```  
    Console.WriteLine("{0}, {1} {2}", student.Last, student.First, student.Scores[0]);  
    ```  
  
     有关更多信息，请参见[orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。  
  
#### 对结果进行分组  
  
1.  分组是查询表达式中的强大功能。  包含 group 子句的查询将生成一系列组，每个组本身包含一个 `Key` 和一个序列，该序列由该组的所有成员组成。  下面的新查询使用学生的姓的第一个字母作为关键字对学生进行分组。  
  
     [!code-cs[CsLINQGettingStarted#14](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_4.cs)]  
  
2.  请注意，查询的类型现在已更改。  该查询现在生成一系列将 `char` 类型作为关键字的组，以及一系列 `Student` 对象。  由于查询的类型已更改，因此下面的代码也会更改 `foreach` 执行循环：  
  
     [!code-cs[CsLINQGettingStarted#15](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_5.cs)]  
  
3.  按 Ctrl \+ F5 运行该应用程序并在**“控制台”**窗口中查看结果。  
  
     有关更多信息，请参见[group 子句](../../../../csharp/language-reference/keywords/group-clause.md)。  
  
#### 隐式类型化变量  
  
1.  显式编写 `IGroupings` 的 `IEnumerables` 代码很快就会变得乏味。  通过使用 `var`，您可以更方便地编写相同的查询和 `foreach` 循环。  `var` 关键字不会更改对象的类型，它仅指示编译器推断类型。  更改 `studentQuery` 的类型和迭代变量的 `group`到 `var` 并重新运行查询。  请注意，在内部 `foreach` 循环中，迭代变量仍然类型化为 `Student`，而查询仍可像以前一样工作。  将 `s` 迭代变量更改为 `var` 并再次运行查询。  您将看到完全相同的结果。  
  
     [!code-cs[CsLINQGettingStarted#16](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_6.cs)]  
  
     有关 [var](../../../../csharp/language-reference/keywords/var.md) 的更多信息，请参见[隐式类型的局部变量](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
#### 按键值对组进行排序  
  
1.  当您运行前面的查询时，会注意到组没有按字母顺序排列。  若要改变这种情况，您必须在 `group` 子句后提供 `orderby` 子句。  但要使用 `orderby` 子句，您首先需要一个标识符，用作对 `group` 子句创建的组的引用。  可以使用 `into` 关键字来提供此标识符，如下所示：  
  
     [!code-cs[csLINQGettingStarted#17](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_7.cs)]  
  
     当您运行此查询时，就会看到组现在已按字母顺序排序。  
  
#### 使用 let 引入标识符  
  
1.  您可以使用 `let` 关键字为查询表达式中的任何表达式结果引入标识符。  此标识符可以提供方便（如下面的示例所示），也可以通过存储表达式的结果来避免多次计算，从而提高性能。  
  
     [!code-cs[csLINQGettingStarted#18](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_8.cs)]  
  
     有关更多信息，请参见[let 子句](../../../../csharp/language-reference/keywords/let-clause.md)。  
  
#### 在查询表达式中使用方法语法  
  
1.  如[Query Syntax and Method Syntax in LINQ](../../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md) 中所述，一些查询操作只能使用方法语法表示。  下面的代码计算源序列中每个 `Student` 的总分，然后对该查询的结果调用 `Average()` 方法来计算班级的平均分。  请注意，查询表达式的两边使用了括号。  
  
     [!code-cs[csLINQGettingStarted#19](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_9.cs)]  
  
#### 在 select 子句中转换或投影  
  
1.  查询生成的序列的元素与源序列中的元素不同，这种情况很常见。  删除或注释掉您之前的查询和执行循环，并用下面的代码替换它。  请注意，该查询返回一个字符串（而非 `Students`）序列，这种情况将反映在 `foreach` 循环中。  
  
     [!code-cs[csLINQGettingStarted#20](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_10.cs)]  
  
2.  本演练前面的代码指出班级的平均分约为 334 分。  若要生成总分高于班级平均分的 `Students` 及其 `Student ID` 的序列，可以在 `select` 语句中使用匿名类型：  
  
     [!code-cs[csLINQGettingStarted#21](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/walkthrough-writing-queries-linq_11.cs)]  
  
## 后续步骤  
 熟悉了在 C\# 中使用查询的基本情况后，便可以开始阅读您感兴趣的具体类型的 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] 提供程序的文档和示例：  
  
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)  
  
 [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md)  
  
 [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)  
  
 [LINQ to Objects](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)  
  
## 请参阅  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Supplementary LINQ Resources](../Topic/Supplementary%20LINQ%20Resources.md)   
 [演练：用 Visual Basic 编写查询](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)