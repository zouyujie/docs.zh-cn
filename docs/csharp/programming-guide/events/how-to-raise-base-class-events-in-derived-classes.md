---
title: "如何：在派生类中引发基类事件（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "事件 [C#], 在派生类中"
ms.assetid: 2d20556a-0aad-46fc-845e-f85d86ea617a
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：在派生类中引发基类事件（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

以下简单示例演示了在基类中声明可从派生类引发的事件的标准方法。  此模式广泛应用于 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 类库中的 Windows 窗体类。  
  
 在创建可用作其他类的基类的类时，应考虑如下事实：事件是特殊类型的委托，只可以从声明它们的类中调用。  派生类无法直接调用基类中声明的事件。  尽管有时需要事件仅由基类引发，但在大多数情形下，应该允许派生类调用基类事件。  为此，您可以在包含该事件的基类中创建一个受保护的调用方法。  通过调用或重写此调用方法，派生类便可以间接调用该事件。  
  
> [!NOTE]
>  不要在基类中声明虚拟事件，也不要在派生类中重写这些事件。  C\# 编译器无法正确处理这些事件，并且无法预知的该派生的事件的用户是否真正订阅了基类事件。  
  
## 示例  
 [!code-cs[csProgGuideEvents#1](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-raise-base-class-events-in-derived-classes_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)   
 [委托](../../../visual-basic/reference/command-line-compiler/index.md)   
 [访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [在 Windows 窗体中创建事件处理程序](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md)