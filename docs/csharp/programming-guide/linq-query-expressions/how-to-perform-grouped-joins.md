---
redirect_url: /dotnet/articles/csharp/linq/perform-grouped-joins
caps.handback.revision: 23
---
# 如何：执行分组联接（C# 编程指南）
分组联接可用于产生分层数据结构。  它将第一个集合中的每个元素与第二个集合中的一组相关元素进行配对。  
  
 例如，一个名为 Student 的类或关系数据库表可能包含两个字段：Id 和 Name。  另一个名为 Course 的类或关系数据库表可能包含两个字段：StudentId 和 CourseTitle。  这两个数据源的分组联接（基于匹配的 Student.Id 和 Course.StudentId）会将每个 Student 与一个 Course 对象集合（可能为空）组合在一起。  
  
> [!NOTE]
>  第一个集合中的每个元素都会出现在分组联接的结果集内，而无论是否在第二个集合中找到相关元素。  如果未找到相关元素，则该元素的相关元素序列为空。  因此，结果选择器可以访问第一个集合的每个元素。  非分组联接中的结果选择器与此不同，它无法访问第一个集合中的那些在第二个集合中没有匹配元素的元素。  
  
 本主题中的第一个示例演示如何执行分组联接；  第二个示例演示如何使用分组联接创建 XML 元素。  
  
## 示例  
  
### 分组联接示例  
 下面的示例根据与 `Pet.Owner` 属性匹配的 `Person` 来对 `Person` 和 `Pet` 类型的对象执行分组联接。  与为每个匹配产生一对元素的非分组联接不同，分组联接只为第一个集合的每个元素产生一个结果对象（在此示例中为一个 `Person` 对象）。  第二个集合中的相应元素（在此示例中为 `Pet` 对象）被分组到一个集合中。  最后，结果选择器函数为每个包含 `Person.FirstName` 和一个 `Pet` 对象集合的匹配创建一个匿名类型。  
  
 [!code-cs[CsLINQProgJoining#5](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/Joins/joins.cs#5)]  
  
## 示例  
  
### 执行分组联接以创建 XML 的示例  
 分组联接非常适合于使用 [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] 来创建 XML。  下面的示例与上一个示例类似，不同之处在于：结果选择器函数创建表示已联接对象的 XML 元素，而不是创建匿名类型。  有关 [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)]的更多信息，请参见[LINQ to XML](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)。  
  
 [!code-cs[CsLINQProgJoining#6](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/Joins/joins.cs#6)]  
  
## 编译代码  
  
-   在 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 中创建一个新的**“控制台应用程序”项目**。  
  
-   添加一个对 System.Core.dll 的引用和一个对 System.Xml.Linq.dll 的引用（如果它们尚未被引用的话）。  
  
-   包括 <xref:System.Linq> 和 <xref:System.Xml.Linq> 命名空间。  
  
-   从示例中复制代码，并将其粘贴到 program.cs 文件中的 `Main` 方法之下。  向 `Main` 方法添加一行代码，以调用粘入的方法。  
  
-   运行该程序。  
  
## 请参阅  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [如何：执行左外部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [LINQ to XML](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)