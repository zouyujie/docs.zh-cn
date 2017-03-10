---
title: "运行时中的泛型（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "泛型 [C#], 在运行时"
ms.assetid: 119df7e6-9ceb-49df-af36-24f8f8c0747f
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# 运行时中的泛型（C# 编程指南）
将泛型类型或方法编译为 Microsoft 中间语言 \(MSIL\) 时，它包含将其标识为具有类型参数的元数据。  泛型类型的 MSIL 的使用因所提供的类型参数是值类型还是引用类型而不同。  
  
 第一次用值类型作为参数来构造泛型类型时，运行时会创建专用泛型类型，将提供的参数代入到 MSIL 中的适当位置。  对于每个用作参数的唯一值类型，都会创建一次专用泛型类型。  
  
 例如，假设您的程序代码声明了一个由整数构造的堆栈：  
  
 [!code-cs[csProgGuideGenerics#42](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-in-the-run-time_1.cs)]  
  
 在此位置，运行时生成 <xref:System.Collections.Generic.Stack%601> 类的专用版本，并相应地用整数替换其参数。  现在，只要程序代码使用整数堆栈，运行时就会重用生成的专用 <xref:System.Collections.Generic.Stack%601> 类。  在下面的示例中，创建了整数堆栈的两个实例，它们共享 `Stack<int>` 代码的单个实例：  
  
 [!code-cs[csProgGuideGenerics#43](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-in-the-run-time_2.cs)]  
  
 但是，假定在代码中的另一个位置创建了使用不同值类型（比如 `long` 或用户定义的结构）作为其参数的另一个 <xref:System.Collections.Generic.Stack%601> 类。  因此，运行时将生成另一个版本的泛型类型，并在 MSIL 中的适当位置替换 `long`。  由于每个专用泛型类本身就包含值类型，因此不再需要转换。  
  
 对于引用类型，泛型的工作方式略有不同。  第一次使用任何引用类型构造泛型类型时，运行时会创建专用泛型类型，用对象引用替换 MSIL 中的参数。  然后，每次使用引用类型作为参数来实例化构造类型时，无论引用类型的具体类型是什么，运行时都会重用以前创建的泛型类型的专用版本。  之所以可以这样，是因为所有引用的大小相同。  
  
 例如，假设您有两个引用类型：一个 `Customer` 类和一个 `Order` 类，并且同时假设您创建了一个 `Customer` 类型的堆栈：  
  
 [!code-cs[csProgGuideGenerics#47](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-in-the-run-time_3.cs)]  
  
 [!code-cs[csProgGuideGenerics#44](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-in-the-run-time_4.cs)]  
  
 此时，运行时将生成 <xref:System.Collections.Generic.Stack%601> 类的一个专用版本，该版本存储稍后将填写的对象引用，而不是存储数据。  假设下一行代码创建另一个引用类型的堆栈，该堆栈名为 `Order`：  
  
 [!code-cs[csProgGuideGenerics#45](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-in-the-run-time_5.cs)]  
  
 不同于值类型，对于 `Order` 类型不创建 <xref:System.Collections.Generic.Stack%601> 类的另一个专用版本。  而是创建 <xref:System.Collections.Generic.Stack%601> 类的一个专用版本实例，并将 `orders` 变量设置为引用它。  假设接下来您遇到一行创建 `Customer` 类型堆栈的代码：  
  
 [!code-cs[csProgGuideGenerics#46](../../../csharp/programming-guide/generics/codesnippet/csharp/generics-in-the-run-time_6.cs)]  
  
 与前面使用 `Order` 类型创建的 <xref:System.Collections.Generic.Stack%601> 类一样，创建了专用 <xref:System.Collections.Generic.Stack%601> 类的另一个实例。  包含在其中的指针设置为引用 `Customer` 类型大小的内存区域。  因为引用类型的数量会随程序的不同而大幅变化，C\# 泛型实现将编译器为引用类型的泛型类创建的专用类的数量减小到一个，从而大幅减小代码量。  
  
 此外，使用值类型或引用类型参数实例化泛型 C\# 类时，反射可以在运行时查询它，并且可以确定它的实际类型及其类型参数。  
  
## 请参阅  
 <xref:System.Collections.Generic>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [泛型](../Topic/Generics%20in%20the%20.NET%20Framework.md)