---
title: "What&#39;s New for Visual C# | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: 9f18dc26-27fa-4603-a639-b573f07a117b
caps.latest.revision: 39
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 39
---
# What&#39;s New for Visual C# #
此页列出每个 C\# 版本的重要功能名以及该语言最新版本中的新功能和增强功能的说明。  
  
## 早期版本  
 C\# 1，Visual Studio .NET 2002  
 首次发布  
  
 C\# 1.1，Visual Studio .NET 2003  
 `#line` 杂注和 xml 文档注释  
  
 C\# 2，Visual Studio .NET 2005  
 匿名方法、泛型、可以为 null 的类型、迭代器\/yield、`static` 类、委托的协变\/逆变  
  
 C\# 3，Visual Studio .NET 2008  
 对象和集合初始值设定项、lambda 表达式、扩展方法、匿名类型、自动属性、语言集成查询 \(LINQ\)、匿名类型、本地 `var` 类型推理、LINQ  
  
 C\# 4，Visual Studio .NET 2010  
 `Dynamic`、命名参数、可选参数、泛型协变\/逆变  
  
 C\# 5，Visual Studio .NET 2012  
 `Async`\/`await`、调用方信息属性  
  
 Visual Studio .NET 2013  
 Bug 修复、性能改进以及 .NET Compiler Platform \("Roslyn"\) 的技术预览  
  
 C\# 6，Visual Studio .NET 2015  
 当前版本，请参阅下文  
  
## 当前版本  
 [nameof](../../csharp/language-reference/keywords/nameof.md)  
 可以在错误消息中使用类型或成员的非限定字符串名，而无需对字符串进行硬编码。  这使代码可以在重构时保持正确。  此功能也可用于挂接“模型\-视图\-控制器”MVC 链接并触发属性更改事件。  
  
 [字符串内插](../../csharp/language-reference/keywords/interpolated-strings.md)  
 可以使用字符串内插表达式构造字符串。  内插字符串表达式类似于包含表达式的模板字符串。  C\# 通过将表达式替换为表达式结果的 ToString 表示形式来创建字符串。  与[复合格式设置](../Topic/Composite%20Formatting.md)相比，内插字符串在参数方面更易于理解。  
  
 [Null 条件成员访问和索引编制](../../csharp/language-reference/operators/null-conditional-operators.md)  
 可以在执行成员访问 \(`?.`\) 或索引 \(`?[]`\) 操作之前以非常轻量的语法方式测试是否存在 null。  这些运算符可帮助编写更少的代码来处理 null 检查，尤其是对于下降到数据结构。  如果左操作数或对象引用为 null，则操作会返回 null。  
  
 [索引初始值设定项](../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)  
 现在可以初始化支持索引编制的集合的特定元素（如初始化字典）。  
  
 [集合初始值设定项和 Add 扩展方法](../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)  
 现在可以在集合具有 Add 扩展方法时，对集合使用初始值设定项。  Add 方法以前必须是实例方法。  
  
 **重载决策**  
 编译器改进了重载决策，这会使更多代码恰好按照你希望它具有的行为方式来工作。  你可能不会再注意到问题的一个方面是在采用可以为 null 的值类型的重载之间进行选择时，或是在将方法组（而不是 lambda）传递到采用委托的重载时。  
  
 [异常筛选器](../../csharp/language-reference/keywords/try-catch.md)  
 可以在 `catch` 子句中使用异常筛选器确定 catch 子句是否应处理异常。  没有此功能时，必须重新引发异常，这会剪裁在重新引发的异常中报告的调用堆栈。  
  
 [Catch 和 Finally 块中的 Await](../../csharp/language-reference/keywords/try-catch.md)  
 可以在 `catch` 和 `finally` 子句中使用 `await`。  
  
 [自动属性初始值设定项](../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
 现在可以通过与初始化字段相似的方式来初始化自动属性。  
  
 [仅限 getter 的自动属性](../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
 现在可以定义只读自动属性，而不必使用完整属性语法定义属性。  可以在声明属性的位置或类型的构造函数中初始化属性。  
  
 **具有表达式主体的函数成员**  
 可以采用与用于 lambda 表达式相同的轻量语法，声明具有代码表达式主体的成员。  请参阅[方法](../../csharp/programming-guide/classes-and-structs/methods.md)、[属性](../../csharp/programming-guide/classes-and-structs/properties.md)、[索引器](../../csharp/programming-guide/indexers/index.md)和[可重载运算符](../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)。  
  
 [使用静态对象](../../csharp/language-reference/keywords/using-directive.md)  
 可以导入静态类型的可访问静态成员，以便可以在不使用类型名限定访问的情况下引用成员。  
  
## 请参阅  
 [Visual Studio 2015 中的新增功能](/visual-studio/ide/what-s-new-in-visual-studio-2015)