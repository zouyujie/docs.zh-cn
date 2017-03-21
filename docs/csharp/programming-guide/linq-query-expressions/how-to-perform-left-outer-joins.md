---
redirect_url: /dotnet/articles/csharp/linq/perform-left-outer-joins
caps.handback.revision: 23
---
# 如何：执行左外部联接（C# 编程指南）
左外部联接是这样一个联接：在其中返回第一个集合的每个元素，而无论该元素在第二个集合中是否具有相关元素。  可以使用 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 执行左通过对分组联接的结果调用方法 <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> 外部联接连接。  
  
## 示例  
 下面的示例演示如何对分组联接的结果调用 <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> 方法来执行左外部联接。  
  
 若要生成两个集合的左外部联接，第一步是使用分组联接执行内部联接。  （有关此过程的说明，请参见[如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)。）在此示例中，`Person` 对象的列表内部联接到 `Pet` 对象列表。`Person` 对象的匹配 `Pet.Owner`。  
  
 第二步是在结果集内包含第一个（左）集合的每个元素，即使该元素在右集合中没有匹配的元素也是如此。  这是通过对分组联接中的每个匹配元素序列调用 <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> 来实现的。  在此示例中，<xref:System.Linq.Enumerable.DefaultIfEmpty%2A> 对匹配 `Pet` 对象每个序列。  方法返回一个包含单个集合，因此，如果匹配 `Pet` 对象序列为任何 `Person` 对象为空，从而确保的默认值每 `Person` 对象在结果集合表示。  
  
> [!NOTE]
>  引用类型的默认值为 `null`;因此，该示例检查空在访问每个 `Pet` 集合的每个元素之前引用。  
  
 [!code-cs[CsLINQProgJoining#7](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-left-outer-joins_1.cs)]  
  
## 编译代码  
  
-   在 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 中创建一个新的控制台应用程序项目。  
  
-   添加对 System.Core.dll 的引用（如果尚未引用它的话）。  
  
-   包含 <xref:System.Linq> 命名空间。  
  
-   复制和粘贴该示例的代码添加到 program.cs 文件中，在 `Program` 选件类的 `Main` 方法。  添加代码行。`Main` 方法调用 `LeftOuterJoinExample` 方法。  
  
-   运行该程序。  
  
## 请参阅  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [如何：执行分组联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)