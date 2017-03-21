---
title: "结构和类 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "类 [Visual Basic]"
  - "类 [Visual Basic], 与结构"
  - "结构变量"
  - "结构"
  - "结构, 与类比较"
  - "结构, 结构变量"
ms.assetid: a221e74a-ffcf-4bdc-a0f6-a088a9bf26cc
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 结构和类 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 统一了结构和类的语法，因此两个实体支持的大多数功能都是相同的。  但是，在结构和类之间还有着重要的区别。  
  
 类的优点在于它可以作为引用类型：与将结构变量与它的所有数据一起传递相比，传递引用更有效。  但是，结构不要求在全局堆中分配内存。  
  
 因为不能从结构继承，结构只应当用于不需要扩展的对象。  当希望创建的对象实例较小时使用结构，并要考虑类与结构之间性能特点的对比。  
  
## 相同点  
 结构和类在以下方面相同：  
  
-   两者都属于*“容器”*类型，这意味着它们包含其他以成员形式存在的类型。  
  
-   两者都具有成员，成员可以包括构造函数、方法、属性、字段、常数、枚举、事件和事件处理程序。  但是，不要将这些成员与结构的声明*“元素”*混淆。  
  
-   两者的成员可以分别有不同的访问级别。  例如，一个成员可以声明为 `Public`，而另一个可以声明为 `Private`。  
  
-   都可实现接口。  
  
-   都有共享的构造函数，有或没有参数。  
  
-   两者都可以公开*“默认属性”*，前提是该属性至少带有一个参数。  
  
-   两者都可以声明和引发事件，而且两者都可以声明委托。  
  
## 不同点  
 结构和类在以下方面有所不同：  
  
-   结构是*“值类型”*，而类是*“引用类型”*。  结构类型的变量包含此结构的数据，而不是像类类型那样包含对数据的引用。  
  
-   结构使用堆栈分配，类使用堆分配。  
  
-   所有的结构元素都默认为 `Public`；类变量和常数默认为 `Private`，而其他的类成员默认为 `Public`。  类成员的这一行为提供与 Visual Basic 6.0 默认值系统的兼容。  
  
-   结构必须至少具有一个非共享变量或非共享的非自定义事件元素；而类可以完全是空的。  
  
-   结构元素不可声明为 `Protected`；类成员可以。  
  
-   只有 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md)`Sub` 结构过程才能处理事件，并且只能使用 [AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md) 语句；而任何类过程都可以处理事件，并且可以使用 [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md) 关键字或 `AddHandler` 语句。  有关更多信息，请参见 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)。  
  
-   结构变量声明不能指定初始值设定项或数组初始大小，而类变量声明可以。  
  
-   结构从 <xref:System.ValueType?displayProperty=fullName> 类隐式继承，不能从任何其他类型继承；而类可以从 <xref:System.ValueType?displayProperty=fullName> 以外的其他任何类继承。  
  
-   结构是不可继承的；而类可以继承。  
  
-   结构从不终止，所以公共语言运行时 \(CLR\) 从不对任何结构调用 <xref:System.Object.Finalize%2A> 方法；而类可由垃圾回收器 \(GC\) 终止，当检测到没有剩余的活动引用时，垃圾回收器将对类调用 <xref:System.Object.Finalize%2A>。  
  
-   结构不需要构造函数；而类需要。  
  
-   结构仅当没有参数时可以有非共享的构造函数；类无论有没有参数都可以。  
  
 每一个结构都有不带参数的隐式公共构造函数。  这个构造函数将结构的所有数据元素都初始化为默认值。  不能重定义此行为。  
  
## 实例和变量  
 由于结构是值类型，每个结构变量都永久地绑定到一个单独的结构实例。  而类是引用类型，对象变量可在不同的时间引用各种类实例。  此区别在下列方面影响结构和类的使用：  
  
-   **初始化。**结构变量使用结构的无参数构造函数隐式包含元素的初始化。  因此，`Dim s As struct1` 等效于 `Dim s As struct1 = New struct1()`。  
  
-   **给变量赋值。**当将一个结构变量赋给另一个，或将结构实例传递给过程参数，所有变量元素的当前值都复制到新结构中。  当将一个对象变量赋给另一个，或传递一个对象变量到过程，仅有引用指针被复制。  
  
-   **给 Nothing 赋值。**您可以将值 [Nothing](../../../../visual-basic/language-reference/nothing.md) 赋给结构变量，但实例继续保持与变量的关联。  您仍可以调用变量的方法和访问它的数据元素，但赋值重新初始化了变量元素。  
  
     相比之下，如果将对象变量设为 `Nothing`，将其与任何类实例断开关联，在给它赋予另一个实例前，不能通过变量访问其他成员。  
  
-   **多个实例。**一个对象变量可以有在不同时间赋给它的不同的类实例，多个对象变量可以同时引用同一个类实例。  当通过指向同一实例的另一个变量访问时，更改的类成员的值会影响这些成员。  
  
     但是，结构元素独立存在于其自身实例中。  更改其值不会在其他任何结构变量中反映出来，即使是在同一 `Structure`声明的其他实例中。  
  
-   **相等。**两个结构的相等测试必须以逐个元素地进行测试的方式执行。  可以使用 <xref:System.Object.Equals%2A> 方法来比较两个对象变量。  <xref:System.Object.Equals%2A> 指示两个变量是否指向同一实例。  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [复合数据类型](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [结构和其他编程元素](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)