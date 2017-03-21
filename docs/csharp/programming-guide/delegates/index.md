---
title: "委托（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 委托"
  - "委托 [C#]"
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# 委托（C# 编程指南）
[delegate](../../../csharp/language-reference/keywords/delegate.md) 是表示对具有特定参数列表和返回类型的方法的引用的类型。  在实例化委托时，你可以将其实例与任何具有兼容签名和返回类型的方法相关联。  你可以通过委托实例调用方法。  
  
 委托用于将方法作为参数传递给其他方法。  事件处理程序就是通过委托调用的方法。  你可以创建一个自定义方法，当发生特定事件时，某个类（如 Windows 控件）就可以调用你的方法。  下面的示例演示了一个委托声明：  
  
 [!code-cs[csProgGuideDelegates#20](../../../csharp/programming-guide/delegates/codesnippet/CSharp/index_1.cs)]  
  
 可将任何可访问类或结构中与委托类型匹配的任何方法分配给委托。  该方法可以是静态方法，也可以是实例方法。  这样便能通过编程方式来更改方法调用，还可以向现有类中插入新代码。  
  
> [!NOTE]
>  在方法重载的上下文中，方法的签名不包括返回值。  但在委托的上下文中，签名包括返回值。  换句话说，方法和委托必须具有相同的返回类型。  
  
 将方法作为参数进行引用的能力使委托成为定义回调方法的理想选择。  例如，对比较两个对象的方法的引用可以作为参数传递到排序算法中。  由于比较代码在一个单独的过程中，因此可通过更常见的方式编写排序算法。  
  
## 委托概述  
 委托具有以下属性：  
  
-   委托类似于 C\+\+ 函数指针，但它们是类型安全的。  
  
-   委托允许将方法作为参数进行传递。  
  
-   委托可用于定义回调方法。  
  
-   委托可以链接在一起；例如，可以对一个事件调用多个方法。  
  
-   方法不必与委托类型完全匹配。  有关详细信息，请参阅[在委托中使用变体](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)。  
  
-   C\# 2.0 版引入了[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)的概念，此类方法允许将代码块作为参数传递来代替单独定义的方法。  C\# 3.0 引入了 Lambda 表达式，利用它们可以更简练地编写内联代码块。  匿名方法和 Lambda 表达式（在某些上下文中）都可编译为委托类型。  这些功能现在统称为匿名函数。  有关 lambda 表达式的更多信息，请参见 [匿名函数](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)。  
  
## 本节内容  
  
-   [使用委托](../../../csharp/programming-guide/delegates/using-delegates.md)  
  
-   [When to Use Delegates Instead of Interfaces \(C\# Programming Guide\)](http://msdn.microsoft.com/zh-cn/2e759bdf-7ca4-4005-8597-af92edf6d8f0)  
  
-   [带有命名方法的委托与带有匿名方法的委托](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)  
  
-   [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
-   [在委托中使用变体](../Topic/Using%20Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md)  
  
-   [如何：合并委托（多路广播委托）](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)  
  
-   [如何：声明、实例化和使用委托](../../../csharp/programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 重要章节  
 [C\# 3.0 Cookbook, Third Edition: More than 250 solutions for C\# 3.0 programmers](http://go.microsoft.com/fwlink/?LinkId=195369)中的[Delegates, Events, and Lambda Expressions](http://go.microsoft.com/fwlink/?LinkId=195395)  
  
 [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)中的[Delegates and Events](http://go.microsoft.com/fwlink/?LinkId=195418)  
  
## 请参阅  
 <xref:System.Delegate>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)