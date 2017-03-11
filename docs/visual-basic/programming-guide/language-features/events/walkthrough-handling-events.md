---
title: "演练：处理事件 (Visual Basic) | Microsoft Docs"
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
  - "事件处理程序 [Visual Basic], 演练"
  - "事件处理 [Visual Basic], 演练"
  - "事件 [Visual Basic], 演练"
  - "变量 [Visual Basic], WithEvents"
  - "演练 [Visual Basic], 事件处理"
  - "WithEvents 关键字, 演练"
ms.assetid: f145b3fc-5ae0-4509-a2aa-1ff6934706bd
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 演练：处理事件 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

这是说明如何处理事件的两个主题中的第二个主题。  第一个主题[演练：声明和引发事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)演示如何声明和引发事件。  本节使用该演练中的窗体和类来展示当事件发生时如何进行处理。  
  
 `Widget` 类示例使用传统的事件处理语句。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 提供了其他处理事件的技术。  作为练习，您可以修改该示例以使用 `AddHandler` 和 `Handles` 语句。  
  
### 处理 Widget 类的 PercentDone 事件  
  
1.  在 `Form1` 中插入下列代码：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#4](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Form1.vb#4)]  
  
     `WithEvents` 关键字指定 `mWidget` 变量用于处理对象的事件。  通过提供将从其中创建对象的类的名称来指定对象的类型。  
  
     变量 `mWidget` 在 `Form1` 中声明，因为 `WithEvents` 变量必须是类级变量。  无论要将这些变量放入什么类型的类，都是这样。  
  
     `mblnCancel` 变量用于取消 `LongTask` 方法。  
  
## 编写代码来处理事件  
 在使用 `WithEvents` 声明变量后，变量名称立即显示在类的**“代码编辑器”**左边的下拉列表中。  当选择 `mWidget` 时，`Widget` 类的事件显示在右边的下拉列表中。  选择一个事件就会显示带有 `mWidget` 前缀和下划线的对应的事件过程。  与某 `WithEvents` 变量关联的所有事件过程均以该变量名作为前缀。  
  
#### 处理事件  
  
1.  从**“代码编辑器”**左边的下拉列表中选择 `mWidget`。  
  
2.  从右边的下拉列表中选择 `PercentDone` 事件。  **“代码编辑器”**将打开 `mWidget_PercentDone` 事件过程。  
  
    > [!NOTE]
    >  **“代码编辑器”**对于插入新的事件处理程序很有用，但不是必需的。  在此演练中，仅将事件处理程序直接复制到代码中将更为直接。  
  
3.  将以下代码添加到 `mWidget_PercentDone` 事件处理程序中：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#5](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Form1.vb#5)]  
  
     每当引发 `PercentDone` 事件时，事件过程就会在一个 `Label` 控件中显示完成百分比。  `DoEvents` 方法允许重新绘制标签，并且还为用户提供机会单击**“取消”**按钮。  
  
4.  为 `Button2_Click` 事件处理程序添加下面的代码：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#6](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Form1.vb#6)]  
  
 如果用户在 `LongTask` 运行时单击**“取消”**按钮，则 `Button2_Click` 事件将在 `DoEvents` 语句允许进行事件处理时立即执行。  类级变量 `mblnCancel` 设置为 `True`，然后 `mWidget_PercentDone` 事件测试它并将 `ByRef Cancel` 参数设置为 `True`。  
  
## 将 WithEvents 变量连接到对象  
 现在已设置好 `Form1`，可以处理 `Widget` 对象的事件。  余下的所有工作就是在某处找到一个 `Widget`。  
  
 当在设计时声明 `WithEvents` 变量时，并没有对象与之相关联。  `WithEvents` 变量就像其他任何对象变量一样。  必须创建一个对象并使用 `WithEvents` 变量为其分配一个引用。  
  
#### 创建对象并为其分配一个引用  
  
1.  从**“代码编辑器”**左边的下拉列表中选择 **“\(Form1 事件\)”**。  
  
2.  从右边的下拉列表中选择 `Load` 事件。  **“代码编辑器”**将打开 `Form1_Load` 事件过程。  
  
3.  为 `Form1_Load` 事件过程添加下面的代码以创建 `Widget`：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#7](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Form1.vb#7)]  
  
 当执行这段代码时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将创建一个 `Widget` 对象，并将其事件连接到与 `mWidget` 相关联的事件过程。  自此以后，每当 `Widget` 引发其 `PercentDone` 事件时，就会执行 `mWidget_PercentDone` 事件过程。  
  
#### 调用 LongTask 方法  
  
-   将以下代码添加到 `Button1_Click` 事件处理程序中：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#8](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Form1.vb#8)]  
  
 在调用 `LongTask` 方法之前，必须初始化将显示完成百分比的标签，而且用于取消该方法的类级 `Boolean` 标志必须设置为 `False`。  
  
 调用 `LongTask`，其任务持续时间为 12.2 秒。  每 1\/3 秒引发一次 `PercentDone` 事件。  每次引发该事件时，都会执行 `mWidget_PercentDone` 事件过程。  
  
 当 `LongTask` 完成以后，将测试 `mblnCancel` 以查看 `LongTask` 是否正常结束，或者它是否因为 `mblnCancel` 设置为 `True` 而停止。  仅在前一种情况下才会更新完成百分比。  
  
#### 运行程序  
  
1.  按 F5 键使该项目进入运行模式。  
  
2.  单击**“开始任务”**按钮。  每次引发 `PercentDone` 事件时，都将以任务完成的百分比来更新标签。  
  
3.  单击**“取消”**按钮停止任务。  请注意，当单击**“取消”**按钮时，其外观并不立即更改。  直到 `My.Application.DoEvents` 语句允许进行事件处理时才会发生 `Click` 事件。  
  
    > [!NOTE]
    >  `My.Application.DoEvents` 方法不会完全像窗体那样处理事件。  例如，在此演练中，必须单击**“取消”**按钮两次。  若要允许窗体直接处理事件，可以使用多线程处理。  有关更多信息，请参见[线程](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 您可能发现按 F11 键逐句通过代码（即一次一行）的方式运行程序很有益。  这样可以清楚地看到执行焦点如何进入 `LongTask`，以及每次引发 `PercentDone` 事件以后如何暂时地重新进入 `Form1`。  
  
 如果当执行焦点返回 `Form1` 的代码中时，`LongTask` 方法再次被调用，这时会发生什么情况呢？  在最坏的情况下，如果每次引发该事件时都调用 `LongTask`，那么可能发生堆栈溢出。  
  
 可以通过向 `mWidget` 分配对新 `Widget` 的引用而使 `mWidget` 变量处理另一个 `Widget` 对象的事件。  实际上，可以让 `Button1_Click` 中的代码在每次单击该按钮时实现此操作。  
  
#### 处理另一个小部件的事件  
  
-   将下面一行代码添加到 `Button1_Click` 过程，并放置在 `mWidget.LongTask(12.2, 0.33)` 的紧前面：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#9](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Form1.vb#9)]  
  
 上面的代码在每次单击该按钮时均创建一个新的 `Widget`。  在 `LongTask` 方法完成后，立即释放对该 `Widget` 的引用并销毁 `Widget`。  
  
 `WithEvents` 变量一次只能包含一个对象引用，所以如果向 `mWidget` 分配了另一个 `Widget` 对象，则将不会再处理以前的 `Widget` 对象的事件。  如果 `mWidget` 是唯一包含对旧 `Widget` 的引用的对象变量，则销毁该对象。  如果需要处理几个 `Widget` 对象的事件，则使用 `AddHandler` 语句来分别处理每个对象的事件。  
  
> [!NOTE]
>  可以根据需要声明任意多个 `WithEvents` 变量，但不支持 `WithEvents` 变量的数组。  
  
## 请参阅  
 [演练：声明和引发事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)   
 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)