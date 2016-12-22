---
title: "事件（C# 编程指南） | Microsoft Docs"
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
  - "类 [C#], 事件"
  - "C# 语言, 事件"
  - "事件 [C#]"
ms.assetid: a8e51b22-d294-44fb-9539-0072f06c4cb3
caps.latest.revision: 43
caps.handback.revision: 43
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 事件（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[类](../../../csharp/language-reference/keywords/class.md)或对象可以通过事件向其他类或对象通知发生的相关事情。 发送（或*引发*）事件的类称为“发行者”，接收（或*处理*）事件的类称为“订户”。  
  
 在典型的 C\# Windows 窗体或 Web 应用程序中，可订阅由按钮和列表框等控件引发的事件。 可以使用 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 集成的开发环境 \(IDE\) 来浏览控件发布的事件，并选择想要处理的事件。 IDE 将自动添加空白事件处理程序方法和订阅该事件的代码。 有关详细信息，请参阅[如何：订阅和取消订阅事件](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)。  
  
## 事件概述  
 事件具有以下属性：  
  
-   发行者确定何时引发事件；订户确定对事件作出何种响应。  
  
-   一个事件可以有多个订户。 订户可以处理来自多个发行者的多个事件。  
  
-   没有订户的事件永远也不会引发。  
  
-   事件通常用于表示用户操作，例如单击按钮或图形用户界面中的菜单选项。  
  
-   当事件具有多个订户时，引发该事件时会同步调用事件处理程序。 若要异步调用事件，请参阅 [Calling Synchronous Methods Asynchronously](../Topic/Calling%20Synchronous%20Methods%20Asynchronously.md)。  
  
-   在 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 类库中，事件基于 <xref:System.EventHandler> 委托和 <xref:System.EventArgs> 基类。  
  
## 相关章节  
 有关详细信息，请参见:  
  
-   [如何：订阅和取消订阅事件](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)  
  
-   [如何：发布符合 .NET Framework 准则的事件](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)  
  
-   [如何：在派生类中引发基类事件](../../../csharp/programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md)  
  
-   [如何：实现接口事件](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)  
  
-   [线程同步](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md)  
  
-   [如何：使用字典存储事件实例](../Topic/How%20to:%20Use%20a%20Dictionary%20to%20Store%20Event%20Instances%20\(C%23%20Programming%20Guide\).md)  
  
-   [如何：实现自定义事件访问器](../../../csharp/programming-guide/events/how-to-implement-custom-event-accessors.md)  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## 重要章节  
 [C\# 3.0 手册，第三版：为 C\# 3.0 程序员提供的 250 多个解决方案](http://go.microsoft.com/fwlink/?LinkId=195369)中的[委托、事件和 Lambda 表达式](http://go.microsoft.com/fwlink/?LinkId=195395)  
  
 [Learning C\# 3.0: Master the Fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)（学习 C\# 3.0：掌握 C\# 3.0 的基本知识）中的[委托和事件](http://go.microsoft.com/fwlink/?LinkId=195418)  
  
## 请参阅  
 <xref:System.EventHandler>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [委托](../../../visual-basic/reference/command-line-compiler/index.md)   
 [在 Windows 窗体中创建事件处理程序](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../Topic/Multithreaded%20Programming%20with%20the%20Event-based%20Asynchronous%20Pattern.md)