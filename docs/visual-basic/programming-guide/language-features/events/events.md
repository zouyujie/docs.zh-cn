---
title: "事件 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "02/25/2017"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "事件 [Visual Basic]"
  - "事件 [Visual Basic], 关于事件"
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 事件 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

虽然您可以用一系列按序执行的过程将 [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] 项目形象地表示出来，但实际上，大多数程序是事件驱动的，也就是说，执行流程是由外部发生的事情（称为“事件”）决定的。  
  
 事件是一个信号，它告知应用程序有重要情况发生。  例如，用户单击窗体上的某个控件时，窗体可能会引发一个 `Click` 事件并调用一个处理该事件的过程。  事件还允许在不同任务之间进行通信。  比方说，您的应用程序脱离主程序执行一个排序任务。  若用户取消这一排序，应用程序可以发送一个取消事件让排序过程停止。  
  
## 事件术语和概念  
 本节描述 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中与事件一起使用的术语和概念。  
  
### 声明事件  
 使用 `Event` 关键字在类、结构、模块和接口内部声明事件，如下面的示例所示：  
  
 [!code-vb[VbVbalrEvents#24](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#24)]  
  
### 引发事件  
 事件就像是通告已发生重要情况的消息。  广播该消息的行为称为“引发”事件。  在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中，使用 `RaiseEvent` 语句引发事件，如下面的示例所示：  
  
 [!code-vb[VbVbalrEvents#25](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#25)]  
  
 必须在声明事件的类、模块或结构的范围内引发事件。  例如，派生类不能引发从基类继承的事件。  
  
### 事件发送器  
 任何能引发事件的对象都是事件发送方，也称“事件源”。  窗体、控件和用户定义的对象都是事件发送器。  
  
### 事件处理程序  
 “事件处理程序”是相应事件发生时调用的过程。  您可以将任何带有匹配签名的有效子例程用作事件处理程序。  可是，不能将函数用作事件处理程序，因为它不能将值返回给事件源。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 采用标准命名约定对事件处理程序进行命名，即用下划线将事件发送方和事件的名称组合起来。  例如，名为 `button1` 的按钮的 `Click` 事件应命名为 `Sub button1_Click`。  
  
> [!NOTE]
>  建议使用此命名约定定义您自己事件的事件处理程序，但这并不是必选的方法；您可以使用任何有效的子例程名称。  
  
## 关联事件与事件处理程序  
 在事件处理程序生效之前，首先必须使用 `Handles` 或 `AddHandler` 语句将它与事件关联。  
  
### WithEvents 语句和 Handles 子句  
 `WithEvents` 语句和 `Handles` 子句提供了陈述性指定事件处理程序的方法。  用 `WithEvents` 关键字所声明对象引发的事件可以由任何过程用该事件的 `Handles` 语句来处理，如下面的示例所示：  
  
 [!code-vb[VbVbalrEvents#1](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#1)]  
  
 `WithEvents` 语句和 `Handles` 子句常常是事件处理程序的最佳选择，因为它们所用的声明语法使得对事件处理的编码和调试更加容易，并使人可以更加轻松地阅读它。  可是，要注意使用 `WithEvents` 变量时有以下限制：  
  
-   不能把 `WithEvents` 变量用作对象变量。  即，不能将它声明为 `Object`，在声明变量时必须指定类名称。  
  
-   由于共享事件 `` 未绑定到类实例，所以不能使用 `WithEvents` 以声明方式处理共享事件。  同样，不能使用 `WithEvents` 或 `Handles` 处理来自 `Structure` 的事件。  在这两种情况下，您可以使用 `AddHandler` 语句处理这些事件。  
  
-   不能创建 `WithEvents` 变量数组。  
  
 `WithEvents` 变量允许单个事件处理程序来处理一类或多类事件，或一个或多个事件处理程序来处理同类事件。  
  
 虽然 `Handles` 子句是关联事件与事件处理程序的标准方法，它仅限于在编译时关联事件与事件处理程序。  
  
 在某些情况下，比如，在对待与窗体或控件关联的事件时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会自动引出一个空事件处理程序并将它与某个事件关联。  例如，在设计模式下双击窗体上的命令按钮时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会为命令按钮创建一个空事件处理程序和一个 `WithEvents` 变量，如下面的代码所示：  
  
 [!code-vb[VbVbalrEvents#26](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#26)]  
  
### AddHandler 和 RemoveHandler  
 `AddHandler` 语句与 `Handles` 子句相似，因为两者都允许指定事件处理程序。  可是，`AddHandler` 与 `RemoveHandler` 一起使用时提供了比 `Handles` 子句更大的灵活性，它们允许动态地添加、移除和更改与某事件关联的事件处理程序。  如果想处理共享事件或结构中的事件，则必须使用 `AddHandler`。  
  
 `AddHandler` 使用两个参数：来自事件发送器（如控件）的事件的名称和计算委托的表达式。  使用 `AddHandler` 时不需要显式指定委托类，因为 `AddressOf` 语句总是返回委托的引用。  下面的示例中，事件处理程序与对象引发的事件相互关联：  
  
 [!code-vb[VbVbalrEvents#28](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#28)]  
  
 `RemoveHandler` 将事件从事件处理程序断开，它所用语法与 `AddHandler` 相同。  例如：  
  
 [!code-vb[VbVbalrEvents#29](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#29)]  
  
 在下面的示例中，一个事件处理程序与一个事件关联，并引发了该事件。  事件处理程序捕获该事件并显示消息。  
  
 然后，第一个事件处理程序被移除，改由另一个事件处理程序与该事件关联。  当该事件再次被引发时，系统会显示不同的消息。  
  
 最后，第二个事件处理程序被移除，且第三次引发了该事件。  由于不再有事件处理程序与该事件关联，因此不会执行任何操作。  
  
 [!code-vb[VbVbalrEvents#38](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class2.vb#38)]  
  
## 处理自基类继承的事件  
 派生类（继承某个基类特征的类）能用 `Handles` `MyBase` 语句处理它们的基类所引发的事件。  
  
#### 处理来自基类的事件  
  
-   通过给事件处理程序过程的声明行添加“`Handles MyBase.`*事件名*”语句来声明派生类中的事件处理程序，其中的“*事件名*”是基类中正在处理的事件的名称。  例如：  
  
     [!code-vb[VbVbalrEvents#12](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#12)]  
  
## 相关章节  
  
|标题|说明|  
|--------|--------|  
|[演练：声明和引发事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)|提供有关声明和引发类的事件的分步说明。|  
|[演练：处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)|演示如何编写事件处理程序过程。|  
|[如何：声明自定义事件以避免阻止](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)|演示如何定义自定义事件，此事件允许异步调用其事件处理程序。|  
|[如何：声明自定义事件以节省内存](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)|演示如何定义只在处理事件时使用内存的自定义事件。|  
|[有关 Visual Basic 中继承的事件处理程序的疑难解答](../../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)|列出了由继承的组件中的事件处理程序引发的常见问题。|  
|[事件](../Topic/Handling%20and%20Raising%20Events.md)|提供对 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 中的事件模型的概述。|  
|[在 Windows 窗体中创建事件处理程序](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md)|描述如何处理与 Windows 窗体对象关联的事件|  
|[委托](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)|提供对 Visual Basic 中的委托的概述。|