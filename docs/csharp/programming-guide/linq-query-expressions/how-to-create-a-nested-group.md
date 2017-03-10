---
redirect_url: /dotnet/articles/csharp/linq/create-a-nested-group
caps.handback.revision: 12
---
# 如何：创建嵌套组（C# 编程指南）
下面的示例演示如何在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 查询表达式中创建嵌套组。  对根据学生年级创建的每个组，将根据每个人的姓名进一步划分为小组。  
  
## 示例  
 [!code-cs[csProgGuideLINQ#24](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csrefLINQHowTos.cs#24)]  
  
 请注意，需要使用三个嵌套的 `foreach` 循环来循环访问嵌套组的内部元素。  
  
## 编译代码  
 此示例包含对[如何：查询对象集合](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md)内示例应用程序中定义的对象的引用。  若要编译和运行此方法，请将它粘贴到该应用程序的 `StudentClass` 类中，并且在 `Main` 方法中添加对它的调用。  
  
 在改写此方法以适合您自己的应用程序时，请记住 LINQ 需要 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 3.5 版，并且项目必须包含一个对 System.Core.dll 的引用和一条针对 System.Linq 的 using 指令。  LINQ to SQL、LINQ to XML 和 LINQ to DataSet 类型需要其他 using 指令和引用。  有关更多信息，请参见 [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md)。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)