---
title: "泛型的优点（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "泛型 [C#], 优点"
ms.assetid: 80f037cd-9ea7-48be-bfc1-219bfb2d4277
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# 泛型的优点（C# 编程指南）
在公共语言运行时和 C\# 语言的早期版本中，通用化是通过在类型与通用基类型 <xref:System.Object> 之间进行强制转换来实现的，泛型提供了针对这种限制的解决方案。  通过创建泛型类，您可以创建一个在编译时类型安全的集合。  
  
 使用非泛型集合类的限制可以通过编写一小段程序来演示，该程序使用 .NET Framework 类库中的 <xref:System.Collections.ArrayList> 集合类。  <xref:System.Collections.ArrayList> 是一个使用起来非常方便的集合类，无需进行修改即可用来存储任何引用或值类型。  
  
 [!code-cs[csProgGuideGenerics#4](../../../csharp/programming-guide/generics/codesnippet/csharp/benefits-of-generics_1.cs)]  
  
 但这种方便是需要付出代价的。  添加到 <xref:System.Collections.ArrayList> 中的任何引用或值类型都将隐式地向上强制转换为 <xref:System.Object>。  如果项是值类型，则必须在将其添加到列表中时进行装箱操作，在检索时进行取消装箱操作。  强制转换以及装箱和取消装箱操作都会降低性能；在必须对大型集合进行循环访问的情况下，装箱和取消装箱的影响非常明显。  
  
 另一个限制是缺少编译时类型检查；因为 <xref:System.Collections.ArrayList> 会将所有项都强制转换为 <xref:System.Object>，所以在编译时无法防止客户端代码执行类似如下的操作：  
  
 [!code-cs[csProgGuideGenerics#5](../../../csharp/programming-guide/generics/codesnippet/csharp/benefits-of-generics_2.cs)]  
  
 尽管将字符串和 `ints` 组合在一个 <xref:System.Collections.ArrayList> 中的做法在创建异类集合时是完全可接受的，并且有时需要有意为之，但这种做法很可能产生编程错误，并且直到运行时才能检测到此错误。  
  
 在 C\# 语言的 1.0 和 1.1 版本中，只能通过编写自己的特定于类型的集合来避免 .NET Framework 基类库集合类中的通用代码的危险。  当然，由于此类不可对多个数据类型重用，因此将丧失通用化的优点，并且您必须对要存储的每个类型重新编写该类。  
  
 <xref:System.Collections.ArrayList> 和其他相似类真正需要的是：客户端代码基于每个实例指定这些类要使用的具体数据类型的方式。  这样将不再需要向上强制转换为 `T:System.Object`，同时，也使得编译器可以进行类型检查。  换句话说，<xref:System.Collections.ArrayList> 需要一个类型参数。  这正是泛型所能提供的。  在 `N:System.Collections.Generic` 命名空间的泛型 <xref:System.Collections.Generic.List%601> 集合中，向集合添加项的操作类似于以下形式：  
  
 [!code-cs[csProgGuideGenerics#6](../../../csharp/programming-guide/generics/codesnippet/csharp/benefits-of-generics_3.cs)]  
  
 对于客户端代码，与 <xref:System.Collections.ArrayList> 相比，使用 <xref:System.Collections.Generic.List%601> 时添加的唯一语法是声明和实例化中的类型参数。  虽然这种方式稍微增加了编码的复杂性，但好处是您可以创建一个比 <xref:System.Collections.ArrayList> 更安全并且速度更快的列表，对于列表项是值类型的情况尤为如此。  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)   
 [Collections Best Practices（有关集合的最佳做法）](http://go.microsoft.com/fwlink/?LinkId=112403)