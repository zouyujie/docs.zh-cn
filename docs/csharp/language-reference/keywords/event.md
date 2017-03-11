---
title: "event（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "event"
  - "remove"
  - "event_CSharpKeyword"
  - "add"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "event 关键字 [C#]"
ms.assetid: 7858fd85-153b-4259-85d0-6aa13c35f174
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# event（C# 参考）
`event` 关键字用于在发行者类中声明事件。  
  
## 示例  
 下面的示例演示如何声明和引发将 <xref:System.EventHandler> 用作基础委托类型的事件。  有关演示如何使用泛型 <xref:System.EventHandler%601> 委托类型、如何订阅事件以及如何创建事件处理程序方法的完整代码示例，请参见[如何：发布符合 .NET Framework 准则的事件](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)。  
  
 [!code-cs[csrefKeywordsModifiers#7](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#7)]  
  
 事件是特殊类型的多路广播委托，仅可从声明它们的类或结构（发行者类）中调用。  如果其他类或结构订阅了该事件，则当发行者类引发该事件时，会调用其事件处理程序方法。  有关更多信息和代码示例，请参见[事件](../../../csharp/programming-guide/events/index.md) 和[委托](../../../csharp/programming-guide/delegates/index.md)。  
  
 事件可标记为 [public](../../../csharp/language-reference/keywords/public.md)、[private](../../../csharp/language-reference/keywords/private.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md) 或 `protected` `internal`。  这些访问修饰符定义类的用户访问事件的方式。  有关更多信息，请参见 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
## 关键字和事件  
 下面的关键字可应用于事件。  
  
|关键字|说明|更多信息|  
|---------|--------|----------|  
|[static](../../../csharp/language-reference/keywords/static.md)|即使类没有实例，调用方也能在任何时候使用该事件。|[静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)|  
|[virtual](../../../csharp/language-reference/keywords/virtual.md)|允许派生类通过使用 [override](../../../csharp/language-reference/keywords/override.md) 关键字来重写事件行为。|[继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)|  
|[sealed](../../../csharp/language-reference/keywords/sealed.md)|指定对于派生类它不再属虚拟性质。||  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|编译器不会生成 `add` 和 `remove` 事件访问器块，因此派生类必须提供自己的实现。||  
  
 通过使用 [static](../../../csharp/language-reference/keywords/static.md) 关键字，可以将事件声明为静态事件。  即使类没有任何实例，调用方也能在任何时候使用静态事件。  有关更多信息，请参见 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
 通过使用 [virtual](../../../csharp/language-reference/keywords/virtual.md) 关键字，可以将事件标记为虚拟事件。  这样，派生类就可以通过使用 [override](../../../csharp/language-reference/keywords/override.md) 关键字来重写事件行为。  有关更多信息，请参见 [继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  重写虚事件的事件也可以为 [sealed](../../../csharp/language-reference/keywords/sealed.md)，以表示其对于派生类不再是虚事件。  最后，可以将事件声明为 [abstract](../../../csharp/language-reference/keywords/abstract.md)，这意味着编译器不会生成 `add` 和 `remove` 事件访问器块。  因此派生类必须提供其自己的实现。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 [C\# 参考](../../../csharp/language-reference/index.md)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [C\# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [添加](../../../csharp/language-reference/keywords/add.md)   
 [移除](../../../csharp/language-reference/keywords/remove.md)   
 [修饰符](../../../csharp/language-reference/keywords/modifiers.md)   
 [如何：合并委托（多路广播委托）](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)