---
redirect_url: /dotnet/articles/csharp/linq/return-a-query-from-a-method
caps.handback.revision: 11
---
# 如何：从方法中返回查询（C# 编程指南）
此示例演示如何从某一方法以返回值和 `out` 参数的形式返回查询。  
  
 任何查询的类型都必须为 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601>，或一种派生类型（如 <xref:System.Linq.IQueryable%601>）。  因此，返回查询的方法的任何返回值或 `out` 参数也必须具有该类型。  如果某个方法将查询具体化为具体的 <xref:System.Collections.Generic.List%601> 或 <xref:System.Array> 类型，则认为该方法在返回查询结果（而不是查询本身）。  仍然能够编写或修改从方法返回的查询变量。  
  
## 示例  
 在下面的示例中，第一个方法以返回值的形式返回查询，第二个方法以 `out` 参数的形式返回查询。  请注意，在这两种情况下，返回的都是查询，而不是查询结果。  
  
 [!code-cs[csProgGuideLINQ#80](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#80)]  
  
## 编译代码  
  
-   创建面向 .NET Framework 3.5 或更高版本的 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 项目。  默认情况下，该项目具有一个对 System.Core.dll 的引用以及一条针对 System.Linq 命名空间的 `using` 指令。  
  
-   将类替换为示例中的代码。  
  
-   按 F5 编译并运行程序。  
  
-   按任意键退出控制台窗口。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)