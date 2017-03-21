---
redirect_url: /dotnet/articles/csharp/linq/perform-inner-joins
caps.handback.revision: 25
---
# 如何：执行内部联接（C# 编程指南）
按照关系数据库的说法，“内部联接”产生一个结果集，对于该结果集内第一个集合中的每个元素，只要在第二个集合中存在一个匹配元素，该元素就会出现一次。  如果第一个集合中的某个元素没有匹配元素，则它不会出现在结果集内。  <xref:System.Linq.Enumerable.Join%2A> 方法（通过 C\# 中的 `join` 子句调用）可实现内联。  
  
 本主题演示如何执行内部联接的四种变体：  
  
-   简单的内部联接，它基于一个简单的键将来自两个数据源的元素相互关联。  
  
-   内部联接，它基于一个复合键将来自两个数据源的元素相互关联。  使用复合键（即由多个值组成的键）可以基于多个属性将元素相互关联。  
  
-   多联接，在其中连续的联接操作被相互拼接在一起。  
  
-   通过使用分组联接实现的内部联接。  
  
## 示例  
  
## 简单键联接示例  
 下面的示例创建了两个集合，其中分别包含以下两个用户定义类型的对象：`Person` 和 `Pet`。  查询使用 C\# 中的 `join` 子句来将 `Person` 对象与 `Pet` 对象（其 `Owner` 为该 `Person`）进行匹配。  C\# 中的 `select` 子句可定义生成的对象的外观。  在此示例中，生成的对象是由主人的名字和宠物的名字组成的匿名类型。  
  
 [!code-cs[CsLINQProgJoining#1](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_1.cs)]  
  
 请注意，其 `LastName` 为“Huff”的 `Person` 对象未出现在结果集内，因为不存在 `Pet.Owner` 等于该 `Person` 的 `Pet` 对象。  
  
## 示例  
  
## 复合键联接示例  
 与仅仅基于一个属性将元素相互关联不同，使用复合键可基于多个属性来比较元素。  为此，需要为每个集合指定键选择器函数，以便返回一个由要比较的属性组成的匿名类型。  如果给属性加上了标签，则这些属性必须在每个键的匿名类型中都有相同的标签，  而且还必须以相同顺序出现。  
  
 下面的示例使用一个 `Employee` 对象列表和一个 `Student` 对象列表来确定哪些雇员同时还是学生。  这两个类型都具有 <xref:System.String> 类型的 `FirstName` 和 `LastName` 属性。  能够从每个列表的元素创建联接键的函数可返回一个由每个元素的 `FirstName` 和 `LastName` 属性组成的匿名类型。  联接操作比较这些复合键是否相等，并且从每个列表中返回名字和姓氏都匹配的对象对。  
  
 [!code-cs[CsLINQProgJoining#2](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_2.cs)]  
  
## 示例  
  
## 多联接示例  
 可以将任意数量的联接操作拼接在一起以执行多联接。  C\# 中的每一个 `join` 子句都可将指定的数据源与前一个联接的结果相互关联。  
  
 下面的示例创建了三个集合：一个 `Person` 对象列表、一个 `Cat` 对象列表以及一个 `Dog` 对象列表。  
  
 C\# 中的第一个 `join` 子句将基于匹配 `Cat.Owner` 的 `Person` 对象对主人和猫进行匹配。  并返回包含 `Person` 对象和 `Cat.Name` 的匿名类型的序列。  
  
 C\# 中的第二个 `join` 子句基于一个组合键将第一个联接返回的匿名类型与所提供的犬列表中的 `Dog` 对象相互关联，该组合键由类型为 `Person` 的 `Owner` 属性和动物名字的首字母组成。  该子句返回一个匿名类型序列，这些类型包含每个匹配对中的 `Cat.Name` 和 `Dog.Name` 属性。  由于这是一个内部联接，因此仅返回第一个数据源中那些在第二个数据源中具有匹配对象的对象。  
  
 [!code-cs[CsLINQProgJoining#3](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_3.cs)]  
  
## 示例  
  
## 使用分组联接实现内部联接的示例  
 下面的示例演示如何使用分组联接来实现内部联接。  
  
 在 `query1` 中，`Person` 对象列表基于与 `Pet.Owner` 属性匹配的 `Person` 分组联接到 `Pet` 对象列表。  分组联接创建了一个中间组集合，该集合中的每个组都由一个 `Person` 对象和匹配的 `Pet` 对象序列组成。  
  
 通过向查询中添加另一个 `from` 子句，此序列的序列被组合（或展平）为一个较长的序列。  最终序列的元素类型由 `select` 子句指定。  在此示例中，该类型是由每个匹配对的 `Person.FirstName` 和 `Pet.Name` 属性组成的匿名类型。  
  
 `query1` 的结果等效于使用 `join` 子句所获得的结果集，而没有 `into` 子句执行内联。  `query2` 变量演示了这一等效查询。  
  
 [!code-cs[CsLINQProgJoining#4](../../../csharp/programming-guide/linq-query-expressions/codesnippet/CSharp/how-to-perform-inner-joins_4.cs)]  
  
## 编译代码  
  
-   在 [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)] 中创建一个新的控制台应用程序项目。  
  
-   添加对 System.Core.dll 的引用（如果尚未引用它的话）。  
  
-   包含 <xref:System.Linq> 命名空间。  
  
-   从示例中复制代码，并将其粘贴到 program.cs 文件中的 `Main` 方法之下。  向 `Main` 方法添加一行代码，以调用粘入的方法。  
  
-   运行该程序。  
  
## 请参阅  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [如何：执行分组联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [如何：执行左外部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [如何：联接两个集合](../Topic/How%20to:%20Join%20Two%20Collections%20\(C%23\)%20\(LINQ%20to%20XML\).md)   
 [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)