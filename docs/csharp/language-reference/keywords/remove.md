---
title: "remove（C# 参考） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "remove_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "remove 事件访问器 [C#]"
ms.assetid: c8223426-c17b-4fe2-8406-01564cf1dd2b
caps.latest.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 8
---
# remove（C# 参考）
`remove` 上下文关键字用于定义一个自定义事件访问器，当客户端代码取消订阅[事件](../../../csharp/language-reference/keywords/event.md)时将调用该访问器。  如果提供自定义 `remove` 访问器，还必须提供 [add](../../../csharp/language-reference/keywords/add.md) 访问器。  
  
## 示例  
 下面的示例演示一个具有自定义 [add](../../../csharp/language-reference/keywords/add.md) 和 `remove` 访问器的事件。  有关完整的示例，请参见[如何：实现接口事件](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)。  
  
 [!code-cs[csrefKeywordsContextual#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/remove_1.cs)]  
  
 通常不需要提供自己的自定义事件访问器。  在大多数情况下，使用在声明事件时由编译器自动生成的访问器就足够了。  
  
## 请参阅  
 [事件](../../../csharp/programming-guide/events/index.md)