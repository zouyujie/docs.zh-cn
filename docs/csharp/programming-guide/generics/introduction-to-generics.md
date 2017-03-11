---
title: "泛型介绍（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "泛型 [C#], 关于泛型"
ms.assetid: a1ad761e-42f7-41dd-a62f-452a2de26b9d
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 32
---
# 泛型介绍（C# 编程指南）
泛型类和泛型方法同时具备可重用性、类型安全和效率，这是非泛型类和非泛型方法无法具备的。  泛型通常用与集合以及作用于集合的方法一起使用。  .NET Framework 2.0 版类库提供一个新的命名空间 <xref:System.Collections.Generic>，其中包含几个新的基于泛型的集合类。  建议面向 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 2.0 及更高版本的所有应用程序都使用新的泛型集合类，而不要使用旧的非泛型集合类如 <xref:System.Collections.ArrayList>。  有关更多信息，请参见 [.NET Framework 类库中的泛型](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md)。  
  
 当然，也可以创建自定义泛型类型和方法，以提供自己的通用解决方案，设计类型安全的高效模式。  下面的代码示例演示一个用于演示用途的简单泛型链接列表类。  （大多数情况下，应使用 .NET Framework 类库提供的 <xref:System.Collections.Generic.List%601> 类，而不是自行创建类。）在通常使用具体类型来指示列表中存储的项的类型的场合，可使用类型参数 `T`。  其使用方法如下：  
  
-   在 `AddHead` 方法中作为方法参数的类型。  
  
-   在 `Node` 嵌套类中作为公共方法 `GetNext` 和 `Data` 属性的返回类型。  
  
-   在嵌套类中作为私有成员数据的类型。  
  
 注意，T 可用于 `Node` 嵌套类。  如果使用具体类型实例化 `GenericList<T>`（例如，作为 `GenericList<int>`），则所有的 `T` 都将被替换为 `int`。  
  
 [!code-cs[csProgGuideGenerics#2](../../../csharp/programming-guide/generics/codesnippet/csharp/introduction-to-generics_1.cs)]  
  
 下面的代码示例演示客户端代码如何使用泛型 `GenericList<T>` 类来创建整数列表。  只需更改类型参数，即可方便地修改下面的代码示例，创建字符串或任何其他自定义类型的列表：  
  
 [!code-cs[csProgGuideGenerics#3](../../../csharp/programming-guide/generics/codesnippet/csharp/introduction-to-generics_2.cs)]  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)