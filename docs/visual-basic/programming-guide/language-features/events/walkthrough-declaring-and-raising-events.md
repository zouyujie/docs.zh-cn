---
title: "演练：声明和引发事件 (Visual Basic) | Microsoft Docs"
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
  - "声明, 事件"
  - "声明事件, 演练"
  - "事件 [Visual Basic], 声明"
  - "事件 [Visual Basic], 引发"
  - "事件 [Visual Basic], 演练"
  - "引发事件, 演练"
ms.assetid: 8ffb3be8-097d-4d3c-b71e-04555ebda2a2
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 演练：声明和引发事件 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

该演练演示如何为名为 `Widget` 的类声明和引发事件。  在完成这些步骤后，您可能需要阅读关联的主题 [演练：处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)，该主题演示在应用程序中如何使用来自 `Widget` 对象的事件提供状态信息。  
  
## Widget 类  
 假定目前有一个 `Widget` 类。  `Widget` 类有一个方法会执行很长时间，您希望应用程序能够提供某种完成状况指示器。  
  
 当然，可以让 `Widget` 对象显示一个完成百分比的对话框，但这样一来，您总是会在使用了 `Widget` 类的每个项目中看到该对话框。  一个好的对象设计原则是让使用对象的应用程序来处理用户界面，除非该对象的整个用途就是管理窗体或对话框。  
  
 `Widget` 的用途是执行其他任务，所以最好添加 `PercentDone` 事件，让调用 `Widget` 的方法的过程来处理该事件和显示状态更新。  `PercentDone` 事件还可以提供取消该任务的机制。  
  
#### 生成此主题的代码示例  
  
1.  打开新的 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] Windows 应用程序项目，并创建一个名为 `Form1` 的窗体。  
  
2.  向 `Form1` 中添加两个按钮和一个标签。  
  
3.  如下表所示命名对象。  
  
    |对象|属性|设置|  
    |--------|--------|--------|  
    |`Button1`|`Text`|开始任务|  
    |`Button2`|`Text`|取消|  
    |`Label`|`(Name)`, `Text`|lblPercentDone, 0|  
  
4.  在**“项目”**菜单上，选择**“添加类”**，在项目中添加名为 `Widget.vb` 的类。  
  
#### 为 Widget 类声明事件  
  
-   使用 `Event` 关键字在 `Widget` 类中声明一个事件。  请注意，事件可以有 `ByVal` 和 `ByRef` 参数，如 `Widget` 的 `PercentDone` 事件所示：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#1](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Widget.vb#1)]  
  
 在调用对象收到 `PercentDone` 事件后，`Percent` 参数即包含任务完成的百分比。  可以将 `Cancel` 参数设置为 `True` 以取消引发该事件的方法。  
  
> [!NOTE]
>  可以声明事件参数，就像声明过程参数一样，但有以下例外：事件不能有 `Optional` 或 `ParamArray` 参数，且事件没有返回值。  
  
 `PercentDone` 事件由 `Widget` 类的 `LongTask` 方法引发。  `LongTask` 采用两个参数：该方法自称要工作的时间长度，以及在 `LongTask` 暂停以引发 `PercentDone` 事件前的最小时间间隔。  
  
#### 引发 PercentDone 事件  
  
1.  要简化对该类使用的 `Timer` 属性的访问，请将一个 `Imports` 语句添加到类模块声明部分的顶部，在 `Class Widget` 语句上面。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#2](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Widget.vb#2)]  
  
2.  将下面的代码添加到 `Widget` 类中：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#3](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Widget.vb#3)]  
  
 在应用程序调用 `LongTask` 方法时，`Widget` 类每隔 `MinimumInterval` 秒就引发 `PercentDone` 事件一次。  该事件返回后，`LongTask` 检查 `Cancel` 参数是否设置为 `True`。  
  
 这里需要几个否认声明。  为简单起见，`LongTask` 过程假定您事先知道任务需要的时间。  但这种情况很少见。  将任务划分为很多大小相等的块很困难，而通常用户最介意的只是在获得有情况发生的指示之前所经过的时间。  
  
 您可能已经发现此示例中的另一个缺陷。  `Timer` 属性返回自午夜以来经过的秒数，因而，如果该应用程序刚好在午夜之前启动，则会承受不住。  更仔细的测量时间的方法会将此类边界条件考虑在内，或者使用诸如 `Now` 之类的属性完全避免此类问题。  
  
 既然 `Widget` 类可引发事件，您就可以进入到下一个演练。  [演练：处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md) 演示如何使用 `WithEvents` 将事件处理程序与 `PercentDone` 事件相关联。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.DateAndTime.Timer%2A>   
 <xref:Microsoft.VisualBasic.DateAndTime.Now%2A>   
 [演练：处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)   
 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)