---
redirect_url: /dotnet/articles/csharp/linq/dynamically-specify-predicate-filters-at-runtime
caps.handback.revision: 22
---
# 如何：在运行时动态指定谓词筛选器（C# 编程指南）
在某些情况下，您直到运行时才能知道必须将多少个谓词应用于 `where` 子句中的源元素。  动态指定多个谓词筛选器的一种方式是使用 <xref:System.Linq.Enumerable.Contains%2A> 方法，如下面的示例中所示。  此示例按两种方式构造。  首先，通过筛选程序中提供的值来运行项目。  然后，使用运行时提供的输入再次运行项目。  
  
### 使用 Contains 方法进行筛选  
  
1.  在 Visual Studio 中，打开一个新的控制台应用程序。  将其命名为 `PredicateFilters`。  
  
2.  从[如何：查询对象集合](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md)中复制 `StudentClass` 类，并将此类粘贴到 `Program` 类下方的命名空间 `PredicateFilters` 中。  `StudentClass` 提供了 `Student` 对象的列表。  
  
3.  将 `StudentClass` 中的 `Main` 方法注释掉。  
  
4.  将 `Program` 类替换为以下代码。  
  
     [!code-cs[csProgGuideLINQ#26](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csrefLINQHowTos.cs#26)]  
  
5.  在 `DynamicPredicates` 类的 `Main` 方法中的 `ids` 声明下添加以下行。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
6.  按 F5 运行项目。  
  
7.  命令提示符窗口中将显示以下输出：  
  
     Garcia: 114  
  
     O'Donnell: 112  
  
     Omelchenko: 111  
  
8.  下一步是重新运行项目，这次使用在运行时输入的输入内容而不是数组 `ids` 来运行项目。  在**“解决方案资源管理器”**中右击**“PredicateFilters”**，然后单击**“属性”**。  
  
9. 单击**“调试”**选项卡。  
  
10. 在**“命令行参数”**窗口中，按如下方式键入 122、117、120 和 115（用空格隔开）：`122 117 120 115`。  在运行项目时，这些值将成为 `Main` 方法的参数 `args` 的元素。  
  
11. 在 `Main` 方法中，将 `QueryByID(ids)` 更改为 `QueryByID(args)`。  
  
12. 按 F5 运行项目。  
  
13. 命令提示符窗口中将显示以下输出：  
  
     Adams: 120  
  
     Feng: 117  
  
     Garcia: 115  
  
     Tucker: 122  
  
### 使用 switch 语句进行筛选  
  
1.  可以使用 `switch` 语句在预先确定的备选查询中进行选择。  在下面的示例中，`studentQuery` 使用的 `where` 子句随着在运行时指定的年级或年份的不同而不同。  
  
2.  复制以下方法并将其粘贴到类 `DynamicPredicates` 中。  
  
     [!code-cs[csProgGuideLINQ#27](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csrefLINQHowTos.cs#27)]  
  
3.  在**“命令行参数”**窗口中，将上一过程中的 ID 号替换为一个介于 1 到 4 之间的整数值。  
  
4.  在 `Main` 方法中，将对 `QueryByID` 的调用替换为以下调用，此调用可将 `args` 数组中的第一个元素作为其参数发送：`QueryByYear(args[0])`。  
  
5.  按 F5 运行项目。  
  
### 在您自己的应用程序中使用此方法  
  
-   在改编此方法以适合您自己的应用程序时，请记住，LINQ 需要版本 3.5 或版本 4 的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)]，并且项目必须包含一个对 System.Core.dll 的引用和一条针对 `System.Linq` 的 `using` 指令。  LINQ to SQL、LINQ to XML 和 LINQ to DataSet 类型需要相应的其他 `using` 指令和引用。  有关更多信息，请参见 [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [where 子句](../../../csharp/language-reference/keywords/where-clause.md)