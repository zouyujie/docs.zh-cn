---
title: "匿名方法（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "匿名方法 [C#]"
  - "委托 [C#], 匿名方法"
  - "方法 [C#], 匿名"
ms.assetid: a62441fa-f0a3-4acb-9aa6-93762a635275
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# 匿名方法（C# 编程指南）
在 2.0 之前的 C\# 版本中，声明[委托](../../../csharp/language-reference/keywords/delegate.md)的唯一方法是使用[命名方法](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)。  C\# 2.0 引入了匿名方法，而在 C\# 3.0 及更高版本中，Lambda 表达式取代了匿名方法，作为编写内联代码的首选方式。  不过，本主题中有关匿名方法的信息同样也适用于 Lambda 表达式。  有一种情况下，匿名方法提供了 Lambda 表达式中所没有的功能。  您可使用匿名方法来忽略参数列表。  这意味着匿名方法可转换为具有各种签名的委托。  这对于 Lambda 表达式来说是不可能的。  有关 lambda 表达式的更多特定信息，请参见 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
 要将代码块传递为委托参数，创建匿名方法则是唯一的方法。  这里是两个示例：  
  
 [!code-cs[csProgGuideDelegates#6](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_1.cs)]  
  
 [!code-cs[csProgGuideDelegates#5](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_2.cs)]  
  
 通过使用匿名方法，由于您不必创建单独的方法，因此减少了实例化委托所需的编码系统开销。  
  
 例如，如果创建方法所需的系统开销是不必要的，则指定代码块（而不是委托）可能非常有用。  启动新线程即是一个很好的示例。  无需为委托创建更多方法，线程类即可创建一个线程并且包含该线程执行的代码。  
  
 [!code-cs[csProgGuideDelegates#7](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_3.cs)]  
  
## 备注  
 匿名方法的参数的范围是“*匿名方法块*”。  
  
 如果目标在块外部，那么，在匿名方法块内使用跳转语句（如 [goto](../../../csharp/language-reference/keywords/goto.md)、[break](../../../csharp/language-reference/keywords/break.md) 或 [continue](../../../csharp/language-reference/keywords/continue.md)）是错误的。  如果目标在块内部，在匿名方法块外部使用跳转语句（如 `goto`、`break` 或 `continue`）也是错误的。  
  
 如果局部变量和参数的范围包含匿名方法声明，则该局部变量和参数称为该匿名方法的“*外部*”变量。  例如，下面代码段中的 `n` 即是一个外部变量：  
  
 [!code-cs[csProgGuideDelegates#8](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_4.cs)]  
  
 外部变量的引用`n`被认为是*捕获*在创建委托时。  与本地变量不同，捕获的变量的生存期内扩展，直到引用该匿名方法委托被垃圾回收。  
  
 匿名方法不能访问外部范围的 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 参数。  
  
 在“*匿名方法块*”中不能访问任何不安全代码。  
  
 在 [is](../../../csharp/language-reference/keywords/is.md) 运算符的左侧不允许使用匿名方法。  
  
## 示例  
 下面的示例演示实例化委托的两种方法：  
  
-   使委托与匿名方法关联。  
  
-   使委托与命名方法 \(`DoWork`\) 关联。  
  
 两种方法都会在调用委托时显示一条消息。  
  
 [!code-cs[csProgGuideDelegates#4](../../../csharp/programming-guide/delegates/codesnippet/CSharp/anonymous-methods_5.cs)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [带有命名方法的委托与带有匿名方法的委托](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)