---
title: "join 子句（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "join"
  - "join_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "join 子句 [C#]"
  - "join 关键字 [C#]"
ms.assetid: 76e9df84-092c-41a6-9537-c3f1cbd7f0fb
caps.latest.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 29
---
# join 子句（C# 参考）
使用 `join` 子句可以将来自不同源序列并且在对象模型中没有直接关系的元素相关联。  唯一的要求是每个源中的元素需要共享某个可以进行比较以判断是否相等的值。  例如，食品经销商可能具有某种产品的供应商列表以及买主列表。  例如，可以使用 `join` 子句创建该产品同一指定地区供应商和买主的列表。  
  
 `join` 子句接受两个源序列作为输入。  每个序列中的元素都必须是可以与另一个序列中的相应属性进行比较的属性，或者包含一个这样的属性。  `join` 子句使用特殊的 `equals` 关键字比较指定的键是否相等。  `join` 子句执行的所有联接都是同等联接。  `join` 子句的输出形式取决于所执行的联接的具体类型。  以下是三种最常见的联接类型：  
  
-   内部联接  
  
-   分组联接  
  
-   左外部联接  
  
## 内部联接  
 下面的示例演示一个简单的内部同等联接。  此查询产生一个“产品名称\/类别”对平面序列。  同一类别字符串将出现在多个元素中。  如果 `categories` 中的某个元素不具有匹配的 `products`，则该类别不会出现在结果中。  
  
 [!code-cs[cscsrefQueryKeywords#24](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Join.cs#24)]  
  
 有关更多信息，请参见 [如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)。  
  
## Group Join  
 含有 `into` 表达式的 `join` 子句称为分组联接。  
  
 [!code-cs[cscsrefQueryKeywords#25](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Join.cs#25)]  
  
 分组联接会产生一个分层的结果序列，该序列将左侧源序列中的元素与右侧源序列中的一个或多个匹配元素相关联。  分组联接没有等效的关系术语；它本质上是一个对象数组序列。  
  
 如果在右侧源序列中找不到与左侧源中的元素相匹配的元素，则 `join` 子句会为该项产生一个空数组。  因此，分组联接基本上仍然是一种内部同等联接，区别只在于分组联接将结果序列组织为多个组。  
  
 如果您只选择分组联接的结果，则可以访问各个项，但无法识别结果所匹配的键。  因此，通常更为有用的做法是选择分组联接的结果并放入一个也具有该键名的新类型中，如上一个示例所示。  
  
 当然，还可以将分组联接的结果用作其他子查询的生成器：  
  
 [!code-cs[cscsrefQueryKeywords#26](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Join.cs#26)]  
  
 有关更多信息，请参见 [如何：执行分组联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)。  
  
## 左外部联接  
 在左外部联接中，将返回左侧源序列中的所有元素，即使它们在右侧序列中没有匹配的元素也是如此。  若要在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 中执行左外部联接，请将 `DefaultIfEmpty` 方法与分组联接结合起来，以指定要在某个左侧元素不具有匹配元素时产生的默认右侧元素。  可以使用 `null` 作为任何引用类型的默认值，也可以指定用户定义的默认类型。  下面的示例演示了用户定义的默认类型：  
  
 [!code-cs[cscsrefQueryKeywords#27](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Join.cs#27)]  
  
 有关更多信息，请参见 [如何：执行左外部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)。  
  
## equals 运算符  
 `join` 子句执行同等联接。  换句话说，只能基于两个键之间的相等关系进行匹配。  其他类型的比较（例如，“greater than”或“not equals”）不受支持。  为了表明所有联接都是同等联接，`join` 子句使用 `equals` 关键字而不是 `==` 运算符。  `equals` 关键字只能用在 `join` 子句中，并且它与 `==` 运算符之间存在一个重要区别。  对于 `equals`，左键使用外部源序列，而右键使用内部源序列。  外部源仅在 `equals` 的左侧位于范围内，而内部源序列仅在其右侧位于范围内。  
  
## 非同等联接  
 通过使用多个 `from` 子句将新序列单独引入到查询中，可以执行非同等联接、交叉联接和其他自定义联接操作。  有关更多信息，请参见 [如何：执行自定义联接操作](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md)。  
  
## 对象集合联接与关系表  
 在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 查询表达式中，联接操作是在对象集合上执行的。  不能使用与两个关系表完全相同的方式“联接”对象集合。  在 [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)] 中，仅当两个源序列没有通过任何关系相互联系时，才需要使用显式 `join` 子句。  使用 [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq-md.md)] 时，外键表在对象模型中表示为主表的属性。  例如，在 Northwind 数据库中，Customer 表与 Orders 表之间具有外键关系。  在将这两个表映射到对象模型时，Customer 类具有一个 Orders 属性，该属性包含与该 Customer 相关联的 Orders 的集合。  实际上，已经为您执行了联接。  
  
 有关在 [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq-md.md)] 的上下文中跨相关表执行查询的更多信息，请参见[如何：映射数据库关系](../Topic/How%20to:%20Map%20Database%20Relationships.md)。  
  
## 复合键  
 使用复合键可以测试多个值是否相等。  有关更多信息，请参见 [如何：使用复合键进行联接](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)。  还可以在 `group` 子句中使用组合键。  
  
## 示例  
 下面的示例比较了使用相同的匹配键对相同数据源执行内部联接、分组联接和左外部联接的结果。  这些示例中添加了一些额外的代码，以便在控制台显示中阐明结果。  
  
 [!code-cs[cscsrefQueryKeywords#23](../../../csharp/language-reference/keywords/codesnippet/csharp/csquerykeywords/Join.cs#23)]  
  
## 备注  
 后面未跟 `into` 的 `join` 子句被转换为 <xref:System.Linq.Enumerable.Join%2A> 方法调用；  后面跟有 `into` 的 `join` 子句被转换为 <xref:System.Linq.Enumerable.GroupJoin%2A> 方法调用。  
  
## 请参阅  
 [查询关键字 \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Join Operations](../../../visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [group 子句](../../../csharp/language-reference/keywords/group-clause.md)   
 [如何：执行左外部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [如何：执行分组联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [如何：对 Join 子句的结果进行排序](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)   
 [如何：使用复合键进行联接](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)   
 [如何：安装示例数据库](../Topic/How%20to:%20Install%20Sample%20Databases.md)