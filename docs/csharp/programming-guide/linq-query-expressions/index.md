---
redirect_url: /dotnet/articles/csharp/linq/index
caps.handback.revision: 21
---
# LINQ 查询表达式（C# 编程指南）
[!INCLUDE[vbteclinqext](../../../csharp/getting-started/includes/vbteclinqext-md.md)] 是一组技术的名称，这些技术建立在将查询功能直接集成到 C\# 语言（以及 Visual Basic 和可能的任何其他 .NET 语言）的基础上。  借助于 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)]，查询现在已是高级语言构造，就如同类、方法、事件等等。  
  
 对于编写查询的开发人员来说，[!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 最明显的“语言集成”部分是查询表达式。  查询表达式是使用 C\# 3.0 中引入的声明性查询语法编写的。  通过使用查询语法，您甚至可以使用最少的代码对数据源执行复杂的筛选、排序和分组操作。  您使用相同的基本查询表达式模式来查询和转换 SQL 数据库、[!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado-md.md)] 数据集、XML 文档和流以及 .NET 集合中的数据。  
  
 下面的示例演示了完整的查询操作。  完整操作包括创建数据源、定义查询表达式，以及在 `foreach` 语句中执行查询。  
  
 [!code-cs[csProgGuideLINQ#11](../../../csharp/programming-guide/arrays/codesnippet/CSharp/index_1.cs)]  
  
 有关 C\# 中的 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 基础知识的更多信息，请参见 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)。  
  
## 查询表达式概述  
  
-   查询表达式可用于查询和转换来自任意支持 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 的数据源中的数据。  例如，单个查询可以从 SQL 数据库检索数据，并生成 XML 流作为输出。  
  
-   查询表达式容易掌握，因为它们使用许多常见的 C\# 语言构造。  有关更多信息，请参见 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)。  
  
-   查询表达式中的变量都是强类型的，但许多情况下您不需要显式提供类型，因为编译器可以推断类型。  有关更多信息，请参见[Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)。  
  
-   在您循环访问 `foreach` 语句中的查询变量之前，不会执行查询。  有关更多信息，请参见 [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)。  
  
-   在编译时，根据 C\# 规范中设置的规则将查询表达式转换为“标准查询运算符”方法调用。  任何可以使用查询语法表示的查询也可以使用方法语法表示。  但是，在大多数情况下，查询语法更易读和简洁。  有关更多信息，请参见 [C\# 语言规范](../../../csharp/language-reference/language-specification.md)和[Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
-   作为编写 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 查询的一项规则，建议尽量使用查询语法，只在必需的情况下才使用方法语法。  这两种不同形式在语义或性能上没有区别。  查询表达式通常比用方法语法编写的等效表达式更易读。  
  
-   一些查询操作，如 <xref:System.Linq.Enumerable.Count%2A> 或 <xref:System.Linq.Enumerable.Max%2A>，没有等效的查询表达式子句，因此必须表示为方法调用。  方法语法可以通过多种方式与查询语法组合。  有关更多信息，请参见[Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)。  
  
-   查询表达式可以编译为表达式树或委托，具体取决于查询所应用到的类型。  <xref:System.Collections.Generic.IEnumerable%601> 查询编译为委托。  <xref:System.Linq.IQueryable> 和 <xref:System.Linq.IQueryable%601> 查询编译为表达式树。  有关更多信息，请参见[表达式树](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 下表列出了一些主题，提供有关常规任务的查询和代码示例的其他信息。  
  
|主题|说明|  
|--------|--------|  
|[查询表达式基础](../../../csharp/programming-guide/linq-query-expressions/query-expression-basics.md)|介绍基本查询概念并提供 C\# 查询语法的示例。|  
|[如何：在 C\# 中编写 LINQ 查询](../../../csharp/programming-guide/linq-query-expressions/how-to-write-linq-queries.md)|提供若干基本查询表达式类型的示例。|  
|[如何：在查询表达式中处理异常](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md)|如何以及何时将可能会引发异常的代码移出查询表达式。|  
|[How to: Populate Object Collections from Multiple Sources \(LINQ\)](../Topic/How%20to:%20Populate%20Object%20Collections%20from%20Multiple%20Sources%20\(LINQ\).md)|如何使用 `select` 语句将来自不同源的数据合并为新类型。|  
|[如何：对查询结果进行分组](../../../csharp/programming-guide/linq-query-expressions/how-to-group-query-results.md)|演示使用 `group` 子句的不同方法。|  
|[如何：创建嵌套组](../../../csharp/programming-guide/linq-query-expressions/how-to-create-a-nested-group.md)|演示如何创建嵌套组。|  
|[如何：对分组操作执行子查询](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)|演示如何使用查询中的子表达式作为新查询的数据源。|  
|[如何：按连续键对结果进行分组](../../../csharp/programming-guide/linq-query-expressions/how-to-group-results-by-contiguous-keys.md)|演示如何实现线程安全的标准查询运算符，该运算符可对流式数据源执行分组操作。|  
|[如何：在运行时动态指定谓词筛选器](../../../csharp/programming-guide/linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)|演示如何为 `where` 子句的相等比较提供任意数目的值。|  
|[如何：在内存中存储查询结果](../../../csharp/programming-guide/linq-query-expressions/how-to-store-the-results-of-a-query-in-memory.md)|阐释如何具体化和存储查询结果，而不必使用 `foreach` 循环。|  
|[如何：从方法中返回查询](../../../csharp/programming-guide/linq-query-expressions/how-to-return-a-query-from-a-method.md)|演示如何从方法返回查询变量，以及如何将它们作为输入参数传递给方法。|  
|[如何：执行自定义联接操作](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md)|演示如何基于任何类型的谓词函数执行联接运算。|  
|[如何：使用复合键进行联接](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)|演示如何基于多个匹配键联接两个源。|  
|[如何：对 Join 子句的结果进行排序](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)|演示如何对联接运算生成的序列进行排序。|  
|[如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)|演示如何在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 中执行内联。|  
|[如何：执行分组联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)|演示如何在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 中生成已分组的联接。|  
|[如何：执行左外部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)|演示如何在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 中生成左外部联接。|  
|[如何：在查询表达式中处理 Null 值](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-null-values-in-query-expressions.md)|演示如何在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 查询中处理 null 值。|  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Walkthrough: Writing Queries in C\#](../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [Basic LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)   
 [Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)   
 [Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [How Linq to Objects Queries Work（Linq to Objects 查询如何工作）](http://go.microsoft.com/fwlink/?LinkId=112389)   
 [Reading and Writing Queries（读取和编写查询）](http://go.microsoft.com/fwlink/?LinkId=112391)   
 [What is a collection?（什么是集合？）](http://go.microsoft.com/fwlink/?LinkId=112394)   
 [Link to Everything: A List of LINQ Providers（所有链接：LINQ 提供程序列表）](http://go.microsoft.com/fwlink/?LinkId=112411)