---
redirect_url: /dotnet/articles/csharp/linq/order-the-results-of-a-join-clause
caps.handback.revision: 6
---
# 如何：对 Join 子句的结果进行排序（C# 编程指南）
此示例演示如何对联接运算的结果进行排序。  请注意，排序是在联接之后执行的。  尽管可以在联接之前将 `orderby` 子句用于一个或多个源序列，但通常我们不建议这样做。  某些 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 提供程序可能不会在联接之后保留排序。  
  
## 示例  
 此查询将创建一个分组联接，然后基于类别元素（仍然在范围中）对组进行排序。  在匿名类型初始值设定项中，子查询将对产品序列中的所有匹配元素进行排序。  
  
 [!code-cs[csProgGuideLINQ#81](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#81)]  
  
## 编译代码  
  
-   创建面向 .NET Framework 3.5 版的 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 项目。  默认情况下，该项目具有一个对 System.Core.dll 的引用以及一条针对 System.Linq 命名空间的 `using` 指令。  
  
-   将代码复制到项目中。  
  
-   按 F5 编译并运行程序。  
  
-   按任意键退出控制台窗口。  
  
## 请参阅  
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [orderby 子句](../../../csharp/language-reference/keywords/orderby-clause.md)   
 [join 子句](../../../csharp/language-reference/keywords/join-clause.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)