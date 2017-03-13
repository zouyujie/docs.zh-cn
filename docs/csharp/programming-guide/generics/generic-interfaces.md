---
title: "泛型接口（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 泛型接口"
  - "泛型 [C#], 接口"
ms.assetid: a8fa49a1-6e78-4a09-87e5-84a0b9f5ffbe
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# 泛型接口（C# 编程指南）
为泛型集合类或表示集合中项的泛型类定义接口通常很有用。  对于泛型类，使用泛型接口十分可取，例如使用 <xref:System.IComparable%601> 而不使用 <xref:System.IComparable>，这样可以避免值类型的装箱和取消装箱操作。  .NET Framework 类库定义了若干泛型接口，以用于 <xref:System.Collections.Generic> 命名空间中的集合类。  
  
 将接口指定为类型参数的约束时，只能使用实现此接口的类型。  下面的代码示例显示从 `SortedList<T>` 类派生的 `GenericList<T>` 类。  有关更多信息，请参见 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)。  `SortedList<T>` 添加约束 `where T : IComparable<T>`。  这将使 `SortedList<T>` 中的 `BubbleSort` 方法能够对列表元素使用泛型 <xref:System.IComparable%601.CompareTo%2A> 方法。  在此示例中，列表元素为简单类，即实现 `Person` 的 `IComparable<Person>`。  
  
 [!code-cs[csProgGuideGenerics#29](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_1.cs)]  
  
 可将多重接口指定为单个类型上的约束，如下所示：  
  
 [!code-cs[csProgGuideGenerics#30](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_2.cs)]  
  
 一个接口可定义多个类型参数，如下所示：  
  
 [!code-cs[csProgGuideGenerics#31](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_3.cs)]  
  
 适用于类的继承规则同样适用于接口：  
  
 [!code-cs[csProgGuideGenerics#32](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_4.cs)]  
  
 如果泛型接口为逆变的，即仅使用其类型参数作为返回值，则此泛型接口可以从非泛型接口继承。  在 .NET Framework 类库中，<xref:System.Collections.Generic.IEnumerable%601> 从 <xref:System.Collections.IEnumerable> 继承，因为 <xref:System.Collections.Generic.IEnumerable%601> 只在 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 的返回值和 <xref:System.Collections.Generic.IEnumerator%601.Current%2A> 属性 getter 中使用 `T`。  
  
 具体类可以实现已关闭的构造接口，如下所示：  
  
 [!code-cs[csProgGuideGenerics#33](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_5.cs)]  
  
 只要类参数列表提供了接口必需的所有参数，泛型类便可以实现泛型接口或已关闭的构造接口，如下所示：  
  
 [!code-cs[csProgGuideGenerics#34](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-interfaces_6.cs)]  
  
 对于泛型类、泛型结构或泛型接口中的方法，控制方法重载的规则相同。  有关更多信息，请参见 [泛型方法](../../../csharp/programming-guide/generics/generic-methods.md)。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [interface](../../../csharp/language-reference/keywords/interface.md)   
 [泛型](../Topic/Generics%20in%20the%20.NET%20Framework.md)