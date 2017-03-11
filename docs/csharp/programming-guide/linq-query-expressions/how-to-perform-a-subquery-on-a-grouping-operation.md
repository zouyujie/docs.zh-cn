---
redirect_url: /dotnet/articles/csharp/linq/perform-a-subquery-on-a-grouping-operation
caps.handback.revision: 15
---
# 如何：对分组操作执行子查询（C# 编程指南）
本主题演示执行以下任务的两种不同方式：创建一个查询，以便将源数据排序到不同的组中，然后分别对每个组执行子查询。  每个示例中的基本技术都是使用一个名为 `newGroup` 的“延续”对源元素进行分组，然后生成一个针对 `newGroup` 的新的子查询。  此子查询是针对外部查询所创建的每个新组运行的。  请注意，在此特定示例中，最终的输出不是组，而是匿名类型的平面序列。  
  
 有关如何分组的更多信息，请参见[group 子句](../../../csharp/language-reference/keywords/group-clause.md)。  
  
 有关延续的更多信息，请参见 [into](../../../csharp/language-reference/keywords/into.md)。  下面的示例使用内存中数据结构作为数据源，但相同的原理适用于任何种类的 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 数据源。  
  
## 示例  
 [!code-cs[csProgGuideLINQ#23](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csrefLINQHowTos.cs#23)]  
  
## 编译代码  
 此示例包含对[如何：查询对象集合](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md)内示例应用程序中定义的对象的引用。  若要编译和运行此方法，请将它粘贴到该应用程序的 `StudentClass` 类中，并且在 `Main` 方法中添加对它的调用。  
  
 在改写此方法以适合您自己的应用程序时，请记住 LINQ 需要 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 3.5 版，并且项目必须包含一个对 System.Core.dll 的引用和一条针对 System.Linq 的 using 指令。  LINQ to SQL、LINQ to XML 和 LINQ to DataSet 类型需要其他 using 指令和引用。  有关更多信息，请参见 [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)