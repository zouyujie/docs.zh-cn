---
redirect_url: /dotnet/articles/csharp/linq/store-the-results-of-a-query-in-memory
caps.handback.revision: 13
---
# 如何：在内存中存储查询结果（C# 编程指南）
查询基本上是一组有关如何检索和组织数据的指令。  若要执行查询，需要调用它的 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法。  当您使用 `foreach` 循环来循环访问元素时，将执行此调用。  若要计算查询和存储其结果，而不执行 `foreach` 循环，请对查询变量调用下列方法之一：  
  
-   <xref:System.Linq.Enumerable.ToList%2A>  
  
-   <xref:System.Linq.Enumerable.ToArray%2A>  
  
-   <xref:System.Linq.Enumerable.ToDictionary%2A>  
  
-   <xref:System.Linq.Enumerable.ToLookup%2A>  
  
 建议在存储查询结果时，将返回的集合对象分配给一个新变量，如下面的示例所示：  
  
## 示例  
 [!code-cs[csProgGuideLINQ#25](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csrefLINQHowTos.cs#25)]  
  
## 编译代码  
  
-   创建面向 .NET Framework 3.5 版的 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 项目。  默认情况下，该项目具有一个对 System.Core.dll 的引用以及一条针对 System.Linq 命名空间的 `using` 指令。  
  
-   将代码复制到项目中。  
  
-   按 F5 编译并运行程序。  
  
-   按任意键退出控制台窗口。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)