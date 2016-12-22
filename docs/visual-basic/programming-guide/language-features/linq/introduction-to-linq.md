---
title: "Visual Basic 中的 LINQ 简介 | Microsoft Docs"
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
  - "延迟执行"
  - "迭代变量"
  - "LINQ"
  - "LINQ [Visual Basic]"
  - "LINQ [Visual Basic], 关于 Visual Basic 中的 LINQ"
  - "查询 [Visual Basic 中的 LINQ], 关于 Visual Basic 中的 LINQ 查询"
  - "查询执行 [Visual Basic 中的 LINQ]"
  - "查询表达式 [Visual Basic 中的 LINQ]"
  - "范围变量"
ms.assetid: 3047d86e-0d49-40e2-928b-dc02e46c7984
caps.latest.revision: 28
caps.handback.revision: 28
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic 中的 LINQ 简介
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

语言集成查询 \(LINQ\) 向 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 添加了查询功能，能够为处理各种数据提供简单而强大的功能。  LINQ 不将查询发送到数据库来处理，也不对搜索的每种类型的数据使用不同的查询语法，而是将查询作为 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 语言的一部分引入。  它使用统一语法，而不考虑数据的类型。  
  
 通过 LINQ，可以查询来自 SQL Server 数据库、XML、内存中数组和集合、[!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] 数据集或支持 LINQ 的任何其他远程或本地数据源的数据。  使用通用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 语言元素即可完成以上所有查询。  因为查询是用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 语言编写的，所以查询结果返回为强类型化对象。  这些对象支持 IntelliSense，这使你能够更快地编写代码，并在编译时（而不是在运行时）捕获查询中的错误。  可将 LINQ 查询用作其他查询的源，以便缩小结果的范围。  还可将它们绑定到控件，使用户能够轻松地查看和修改查询结果。  
  
 例如，下面的代码示例显示一个 LINQ 查询，它从集合返回一个客户列表并根据位置对其进行分组。  
  
 [!code-vb[VbVbalrIntroToLINQ#1](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_1.vb)]  
  
 在本主题中，你将了解有关以下方面的信息：  
  
-   [运行示例](#RunningtheExamples)  
  
-   [LINQ 提供程序](#LINQProviders)  
  
-   [LINQ 查询的结构](#StructureOfALINQQuery)  
  
-   [Visual Basic LINQ 查询运算符](#VisualBasicLINQQueryOperators)  
  
-   [使用 LINQ to SQL 连接到数据库](#ConnectingToADatabase)  
  
-   [支持 LINQ 的 Visual Basic 功能](#VisualBasicFeaturesThatSupportLINQ)  
  
-   [延迟执行和立即执行查询](#QueryExecution)  
  
-   [Visual Basic 中的 XML](#XMLInVisualBasic)  
  
-   [相关资源](#RelatedResources)  
  
-   [“如何”和“演练”主题](#HowToAndWalkthroughTopics)  
  
##  <a name="RunningtheExamples"></a> 运行示例  
 若要运行简介中和“LINQ 查询的结构”部分中的示例，请包含以下代码，它将返回客户和订单的列表。  
  
 [!code-vb[VbVbalrIntroToLINQ#31](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_2.vb)]  
  
##  <a name="LINQProviders"></a> LINQ 提供程序  
 *“LINQ 提供程序”* 将 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] LINQ 查询映射到被查询的数据源。  编写 LINQ 查询时，该提供程序将接受该查询，并将其转换为数据源能够执行的命令。  该提供程序还将来自源的数据转换为构成查询结果的对象。  最后，当你将更新发送至数据源时，它又将这些对象转换为数据。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 包括以下 LINQ 提供程序。  
  
|||  
|-|-|  
|提供程序|描述|  
|LINQ to Objects|通过 LINQ to Objects 提供程序，可以查询内存中集合和数组。  如果对象支持 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601> 接口，则可以通过 LINQ to Objects 提供程序对其进行查询。<br /><br /> 可以通过导入 <xref:System.Linq> 命名空间来启用 LINQ to Objects 提供程序，默认情况下，将为所有 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 项目导入此命名空间。<br /><br /> 有关 LINQ to Objects 提供程序的详细信息，请参阅 [LINQ to Objects](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)。|  
|LINQ to SQL|通过 LINQ to SQL 提供程序，可以查询和修改 SQL Server 数据库中的数据。  这样就可以轻松将应用程序的对象模型映射到数据库中的表和对象。<br /><br /> [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 通过包括对象关系设计器（O\/R 设计器）使其能更轻松地使用 LINQ to SQL。  此设计器用于在应用程序中创建映射到数据库中的对象的对象模型。 O\/R 设计器还提供一项功能，用于将存储过程和函数映射到 <xref:System.Data.Linq.DataContext> 对象，该对象可管理与数据库的通信和存储乐观并发检查的状态。<br /><br /> 有关 LINQ to SQL 提供程序的详细信息，请参阅 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)。  有关对象关系设计器的详细信息，请参阅[对象关系设计器（O\/R 设计器）](/visual-studio/data-tools/linq-to-sql-tools-in-visual-studio2)。|  
|LINQ to XML|通过 LINQ to XML 提供程序，可以查询和修改 XML。  可以修改内存中 XML，也可以从文件加载 XML 以及将 XML 保存到文件。<br /><br /> 此外，LINQ to XML 提供程序还包括 XML 文本和 XML 轴属性，通过它们，你可以在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 代码中直接编写 XML。  有关详细信息，请参阅 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)。|  
|LINQ to DataSet|通过 LINQ to DataSet 提供程序，可以查询和更新 [!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] 数据集中的数据。  可以将 LINQ 的强大功能添加到使用数据集的应用程序，以便简化和扩展查询、聚合和更新数据集中数据的功能。<br /><br /> 有关详细信息，请参阅 [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md)。|  
  
##  <a name="StructureOfALINQQuery"></a> LINQ 查询的结构  
 LINQ 查询（通常称为*“查询表达式”*）由标识数据源和查询的迭代变量的查询子句组合而成。  查询表达式还可以包含排序、筛选、分组和联接的说明或要对源数据应用的计算。  查询表达式语法类似于 SQL的语法；因此，你可能发现该语法大都非常熟悉。  
  
 查询表达式以 `From` 子句开头。  此子句标识查询的源数据和用于分别表示源数据中每个元素的变量。  这些变量叫做*“范围变量”*或*“迭代变量”*。  `From` 子句是查询所必需的，但 `Aggregate` 查询除外，在该查询中 `From` 子句是可选的。  在 `From` 或 `Aggregate` 子句中标识查询的范围和源后，即可包括查询子句的任意组合来优化查询。  有关查询子句的详细信息，请参阅本主题中稍后介绍的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] LINQ 查询运算符。  例如，下面的查询将客户数据源集合标识为 `customers` 变量和一个名为 `cust` 的迭代变量。  
  
 [!code-vb[VbVbalrIntroToLINQ#2](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_3.vb)]  
  
 此示例本身是一个有效查询；但是，如果添加更多查询子句以优化结果，查询将变得更加强大。  例如，可以添加 `Where` 子句，以便按一个或多个值筛选结果。  查询表达式都是单行代码；只能将其他查询子句附加到查询的末尾。  可以使用下划线 \(\_\) 续行符将查询拆散为多行文本，以提高可读性。  下面的代码示例演示了包含 `Where` 子句的查询示例。  
  
 [!code-vb[VbVbalrIntroToLINQ#3](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_4.vb)]  
  
 另一个功能强大的查询子句是 `Select` 子句，它能够从数据源仅返回所选字段。  LINQ 查询返回强类型化对象的可枚举集合。  查询可以返回匿名类型或具名类型的集合。  可以使用 `Select` 子句从数据源仅返回单个字段。  执行此操作时，返回的集合类型为该单个字段的类型。  也可以使用 `Select` 子句从数据源返回多个字段。  执行此操作时，返回的集合类型为新的匿名类型。  还可以将由查询返回的字段和指定的具名类型字段进行匹配。  下面的代码示例演示了一个查询表达式，它返回一个匿名类型的集合，该集合具有使用来自数据源中所选字段的数据填充的成员。  
  
 [!code-vb[VbVbalrIntroToLINQ#4](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_5.vb)]  
  
 还可使用 LINQ 查询合并多个数据源组并返回单个结果。  可以使用一个或多个 `From` 子句，或者使用 `Join` 或 `Group Join` 查询子句来完成此操作。  下面的代码示例演示了一个查询表达式，它合并客户和订单数据，并返回包含客户和订单数据的匿名类型的集合。  
  
 [!code-vb[VbVbalrIntroToLINQ#5](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_6.vb)]  
  
 可以使用 `Group Join` 子句创建包含客户对象集合的分层查询结果。  每个客户对象都具有一个包含该客户所有订单的集合的属性。  下面的代码示例演示了一个查询表达式，它将客户和订单数据合并为分层结果，并返回一个匿名类型的集合。  查询返回一个包括 `CustomerOrders` 属性的类型，该属性包含客户订单数据的集合。  它还包括 `OrderTotal` 属性，该属性包含客户所有订单的总计值之和。  （此查询等效于 LEFT OUTER JOIN。）  
  
 [!code-vb[VbVbalrIntroToLINQ#6](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_7.vb)]  
  
 还有几个其他 LINQ 查询运算符，可用它们创建功能强大的查询表达式。  本主题的下一部分将讨论查询表达式中可以包括的各种查询子句。  有关 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 查询子句的详细信息，请参阅[查询](../../../../visual-basic/language-reference/queries/queries.md)。  
  
##  <a name="VisualBasicLINQQueryOperators"></a> Visual Basic LINQ 查询运算符  
 你可以调用 <xref:System.Linq> 命名空间和支持 LINQ 查询的其他命名空间中的类包括的方法，以便根据应用程序的需要创建和完善查询。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 包括最常见查询子句的关键字，如下表所述。  
  
|||  
|-|-|  
|术语|定义|  
|[From 子句](../../../../visual-basic/language-reference/queries/from-clause.md)|需要 `From` 子句或 `Aggregate` 子句才能开始查询。  `From` 子句可指定查询的源集合和迭代变量。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#7](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_8.vb)]|  
|[Select 子句](../../../../visual-basic/language-reference/queries/select-clause.md)|可选。  声明查询的一组迭代变量。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#8](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_9.vb)]<br /><br /> 如果未指定 `Select` 子句，则该查询的迭代变量将由 `From` 或 `Aggregate` 子句指定的迭代变量组成。|  
|[Where 子句](../../../../visual-basic/language-reference/queries/where-clause.md)|可选。  指定查询的筛选条件。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#9](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_10.vb)]|  
|[Order By 子句](../../../../visual-basic/language-reference/queries/order-by-clause.md)|可选。  指定查询中列的排列顺序。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#10](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_11.vb)]|  
|[Join 子句](../../../../visual-basic/language-reference/queries/join-clause.md)|可选。  将两个集合合并为单个集合。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#11](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_12.vb)]|  
|[Group By 子句](../../../../visual-basic/language-reference/queries/group-by-clause.md)|可选。  对查询结果的元素进行分组。  可用于将聚合函数应用到每个组。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#12](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_13.vb)]|  
|[Group Join 子句](../../../../visual-basic/language-reference/queries/group-join-clause.md)|可选。  将两个集合合并为单个分层集合。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#13](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_14.vb)]|  
|[Aggregate 子句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)|需要 `From` 子句或 `Aggregate` 子句才能开始查询。  `Aggregate` 子句向集合应用一个或多个聚合函数。  例如，可以使用 `Aggregate` 子句计算查询所返回的所有元素之和。<br /><br /> [!code-vb[VbVbalrIntroToLINQ#14](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_15.vb)]<br /><br /> 还可以使用 `Aggregate` 子句来修改查询。  例如，可以使用 `Aggregate` 子句，对相关查询集合执行计算。<br /><br /> [!code-vb[VbVbalrIntroToLINQ#15](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_16.vb)]|  
|[Let 子句](../../../../visual-basic/language-reference/queries/let-clause.md)|可选。  计算一个值，并将其分配到查询中的新变量。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#16](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_17.vb)]|  
|[Distinct 子句](../../../../visual-basic/language-reference/queries/distinct-clause.md)|可选。  限制当前迭代变量的值，以在查询结果中消除重复值。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#17](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_18.vb)]|  
|[Skip 子句](../../../../visual-basic/language-reference/queries/skip-clause.md)|可选。  绕过集合中指定数量的元素，然后返回剩余的元素。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#18](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_19.vb)]|  
|[Skip While 子句](../../../../visual-basic/language-reference/queries/skip-while-clause.md)|可选。  跳过集合中指定条件为 `true` 的任何元素，然后返回剩余元素。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#19](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_20.vb)]|  
|[Take 子句](../../../../visual-basic/language-reference/queries/take-clause.md)|可选。  从集合的开头返回指定数量的连续元素。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#20](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_21.vb)]|  
|[Take While 子句](../../../../visual-basic/language-reference/queries/take-while-clause.md)|可选。  包括集合中指定条件为 `true` 的任何元素，并绕过剩余元素。  例如:<br /><br /> [!code-vb[VbVbalrIntroToLINQ#21](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_22.vb)]|  
  
 有关 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 查询子句的详细信息，请参阅[查询](../../../../visual-basic/language-reference/queries/queries.md)。  
  
 可以通过调用 LINQ 提供的可枚举类型和可查询类型的成员来使用其他 LINQ 查询功能。  可以通过对查询表达式的结果调用特定查询运算符来使用这些附加功能。  例如，下面的代码示例使用 <xref:System.Linq.Enumerable.Union%2A> 方法，将两个查询的结果合并为一个查询结果。  它使用 <xref:System.Linq.Enumerable.ToList%2A> 方法，将查询结果返回为一个泛型列表。  
  
 [!code-vb[VbVbalrIntroToLINQ#22](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/introduction-to-linq_23.vb)]  
  
 有关其他 LINQ 功能的详细信息，请参阅[Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
##  <a name="ConnectingToADatabase"></a> 使用 LINQ to SQL 连接到数据库  
 在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中，可使用 LINQ to SQL 文件标识希望访问的 SQL Server 数据库对象（如表、视图和存储过程）。  LINQ to SQL 文件具有 .dbml 扩展名。  
  
 有效地连接到 SQL Server 数据库时，即可向项目添加**“LINQ to SQL 类”**项模板。  此操作将显示对象关系设计器（O\/R 设计器）。  使用 O\/R 设计器，可以将代码中希望访问的项从**“服务器资源管理器”**\/**“数据库资源管理器”**拖动到设计器图面上。  LINQ to SQL 文件可向项目添加 <xref:System.Data.Linq.DataContext> 对象。  此对象包括你希望访问的表和视图的属性和集合，以及希望调用的存储过程的方法。  保存对 LINQ to SQL \(.dbml\) 文件所作的更改后，即可通过引用由 O\/R 设计器定义的 <xref:System.Data.Linq.DataContext> 对象，在代码中访问这些对象。  项目的 <xref:System.Data.Linq.DataContext> 对象根据 LINQ to SQL 文件的名称进行命名。  例如，名为 Northwind.dbml 的 LINQ to SQL 文件将创建名为 `NorthwindDataContext` 的 <xref:System.Data.Linq.DataContext> 对象。  
  
 有关分步说明的示例，请参阅[如何：查询数据库](../../../../visual-basic/programming-guide/language-features/linq/how-to-query-a-database-by-using-linq.md) 和[如何：调用存储过程](../../../../visual-basic/programming-guide/language-features/linq/how-to-call-a-stored-procedure-by-using-linq.md)。  
  
##  <a name="VisualBasicFeaturesThatSupportLINQ"></a> 支持 LINQ 的 Visual Basic 功能  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 还包括其他值得注意的功能，它们能够简化 LINQ 的使用，并减少执行 LINQ 查询所必须编写的代码量。  这些要求包括：  
  
-   **匿名类型**，可用于根据查询结果创建新类型。  
  
-   **隐式类型化变量**，可用于延迟指定类型，并让编译器根据查询结果推断类型。  
  
-   **扩展方法**，可用于使用你自己的方法扩展现有类型而不修改类型本身。  
  
 有关详细信息，请参阅[Visual Basic Features That Support LINQ](../../../../visual-basic/programming-guide/concepts/linq/features-that-support-linq.md)。  
  
##  <a name="QueryExecution"></a> 延迟执行和立即执行查询  
 执行查询与创建查询相互独立。  创建查询后，通过单独的机制触发其执行。  可以在定义查询后立即执行查询（*“立即执行”*）；或存储定义，稍后再执行查询（*“延迟执行”*）。  
  
 默认情况下，创建查询后，它本身不会立即执行。  而会将查询定义存储在用于引用查询结果的变量中。  当稍后在代码中（如在 `For…Next` 循环中）访问查询结果变量时，将执行该查询。  此过程称为*“延迟执行”*。  
  
 也可在定义查询后立即执行查询，这即是*“立即执行”*。  可以通过应用需要访问查询结果中单个元素的方法来触发立即执行。  包括聚合函数（如 `Count`、`Sum`、`Average`、`Min` 或 `Max`）可产生此结果。  有关聚合函数的详细信息，请参阅 [Aggregate 子句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。  
  
 使用 `ToList` 或 `ToArray` 方法也会强制立即执行。  当你希望立即执行查询并缓存查询结果时，这将很有用。  有关这些方法的详细信息，请参阅[Converting Data Types](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md)。  
  
 有关执行查询的详细信息，请参阅 [编写第一个 LINQ 查询](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)。  
  
##  <a name="XMLInVisualBasic"></a> Visual Basic 中的 XML  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中的 XML 功能包括 XML 文本和 XML 轴属性，可用于在代码中轻松创建、访问、查询和修改 XML。  XML 文本可用于在代码中直接编写 XML。  Visual Basic 编译器将 XML 视为第一类数据对象。  
  
 下面的代码示例演示了如何创建 XML 元素、访问其子元素和属性，以及使用 LINQ 查询该元素的内容。  
  
 [!code-vb[VbXmlSamples#8](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/introduction-to-linq_24.vb)]  
  
 有关详细信息，请参阅 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)。  
  
##  <a name="RelatedResources"></a> 相关资源  
  
|||  
|-|-|  
|主题|说明|  
|[XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)|描述 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中可查询和可将 XML 包括为 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 代码中的第一类数据对象的 XML 功能。|  
|[查询](../../../../visual-basic/language-reference/queries/queries.md)|提供有关 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中可用查询子句的参考信息。|  
|[LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)|包括常规信息、编程指南和 LINQ 示例。|  
|[LINQ to SQL](../Topic/LINQ%20to%20SQL.md)|包括常规信息、编程指南和 LINQ to SQL 示例。|  
|[LINQ to Objects](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)|包括常规信息、编程指南和 LINQ to Objects 示例。|  
|[LINQ to ADO.NET](../Topic/LINQ%20to%20ADO.NET%20\(Portal%20Page\)1.md)|包括常规信息、编程指南和 LINQ to [!INCLUDE[vstecado](../../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] 示例。|  
|[LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)|包括常规信息、编程指南和 LINQ to XML 示例。|  
  
##  <a name="HowToAndWalkthroughTopics"></a> “如何”和“演练”主题  
 [如何：查询数据库](../../../../visual-basic/programming-guide/language-features/linq/how-to-query-a-database-by-using-linq.md)  
  
 [如何：调用存储过程](../../../../visual-basic/programming-guide/language-features/linq/how-to-call-a-stored-procedure-by-using-linq.md)  
  
 [如何：修改数据库中的数据](../../../../visual-basic/programming-guide/language-features/linq/how-to-modify-data-in-a-database-by-using-linq.md)  
  
 [如何：使用联接合并数据](../../../../visual-basic/programming-guide/language-features/linq/how-to-combine-data-with-linq-by-using-joins.md)  
  
 [如何：排序查询结果](../../../../visual-basic/programming-guide/language-features/linq/how-to-sort-query-results-by-using-linq.md)  
  
 [如何：筛选查询结果](../Topic/How%20to:%20Filter%20Query%20Results%20by%20Using%20LINQ%20\(Visual%20Basic\).md)  
  
 [如何：对数据进行计数、求和与求平均值计算](../../../../visual-basic/programming-guide/language-features/linq/how-to-count-sum-or-average-data-by-using-linq.md)  
  
 [如何：查找查询结果中的最小值或最大值](../Topic/How%20to:%20Find%20the%20Minimum%20or%20Maximum%20Value%20in%20a%20Query%20Result%20by%20Using%20LINQ%20\(Visual%20Basic\).md)  
  
 [演练：创建 LINQ to SQL 类（O\/R 设计器）](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)  
  
 [如何：分配存储过程以执行更新、插入和删除（O\/R 设计器）](../Topic/How%20to:%20Assign%20stored%20procedures%20to%20perform%20updates,%20inserts,%20and%20deletes%20\(O-R%20Designer\).md)  
  
## 重要章节  
 [第 17 章：LINQ](http://go.microsoft.com/fwlink/?LinkId=195277)（[Visual Basic 2008 编程](http://go.microsoft.com/fwlink/?LinkId=195383)）  
  
## 请参阅  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Visual Basic 中的 LINQ to XML 概述](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)   
 [LINQ to DataSet 概述](../Topic/LINQ%20to%20DataSet%20Overview.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [LINQ 示例](../Topic/LINQ%20Samples.md)   
 [对象关系设计器（O\/R 设计器）](/visual-studio/data-tools/linq-to-sql-tools-in-visual-studio2)   
 [DataContext 方法（O\/R 设计器）](/visual-studio/data-tools/datacontext-methods-o-r-designer)