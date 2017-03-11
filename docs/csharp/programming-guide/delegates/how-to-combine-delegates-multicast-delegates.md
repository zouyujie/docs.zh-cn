---
title: "如何：合并委托（多路广播委托）（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "委托 [C#], 组合"
  - "多路广播委托 [C#]"
ms.assetid: 4e689450-6d0c-46de-acfd-f961018ae5dd
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# 如何：合并委托（多路广播委托）（C# 编程指南）
本示例演示如何创建多播委托。  [委托](../../../csharp/language-reference/keywords/delegate.md)对象的一个有用属性是：可以使用 `+` 运算符将多个对象分配给一个委托实例。  多播委托包含已分配委托的列表。  在调用多播委托时，它会按顺序调用列表中的委托。  只能合并相同类型的委托。  
  
 `-` 运算符可用于从多播委托中移除组件委托。  
  
## 示例  
 [!code-cs[csProgGuideDelegates#11](../../../csharp/programming-guide/delegates/codesnippet/csharp/csrefDelegates/Delegates.cs#11)]  
  
## 请参阅  
 <xref:System.MulticastDelegate>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)