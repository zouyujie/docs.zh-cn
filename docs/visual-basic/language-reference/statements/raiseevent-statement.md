---
title: "RaiseEvent 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.RaiseEventMethod"
  - "vb.RaiseEvent"
  - "RaiseEvent"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "事件处理程序, 将事件连接到"
  - "RaiseEvent 语句"
  - "引发事件, RaiseEvent 语句"
ms.assetid: f82e380a-1e6b-4047-bea8-c853f4d2c742
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# RaiseEvent 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

触发类、窗体或文档中在模块级声明的事件。  
  
## 语法  
  
```  
RaiseEvent eventname[( argumentlist )]  
```  
  
## 部件  
 `eventname`  
 必选。  要触发的事件的名称。  
  
 `argumentlist`  
 可选。  以逗号分隔的变量、数组或表达式的列表。  `argumentlist` 参数必须括在括号中。  如果没有参数，则必须省略括号。  
  
## 备注  
 必选的 `eventname` 是在模块中声明的事件的名称。  它符合 Visual Basic 变量命名规则。  
  
 如果事件尚未在引发它的模块中声明，则将发生错误。  下面的代码片断阐释了一个事件声明和一个引发该事件的过程。  
  
 [!code-vb[VbVbalrEvents#37](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_1.vb)]  
  
 不能使用 `RaiseEvent` 来引发未在模块中显式声明的事件。  例如，所有窗体从 <xref:System.Windows.Forms.Form?displayProperty=fullName> 继承一个 <xref:System.Windows.Forms.Control.Click> 事件，但不能使用派生窗体中的 `RaiseEvent` 来引发该事件。  如果在窗体模块中声明 `Click` 事件，则该事件将隐藏窗体自身的 <xref:System.Windows.Forms.Control.Click> 事件。  您仍然可以通过调用 <xref:System.Windows.Forms.Control.OnClick%2A> 方法来调用窗体的 <xref:System.Windows.Forms.Control.Click> 事件。  
  
 默认情况下，Visual Basic 中定义的事件会按照建立连接的顺序来引发它的事件处理程序。  由于事件可以具有 `ByRef` 参数，因此，晚期连接的进程可能接收已被早期事件处理程序更改的参数。  事件处理程序执行完毕后，会将控制返回到引发事件的子例程。  
  
> [!NOTE]
>  非共享事件不应该在声明它们的类的构造函数内引发。  虽然这些事件不会导致运行时错误，但它们可能会无法由关联的事件处理程序来捕获。  如果您需要从构造函数中引发事件，请使用 `Shared` 修饰符来创建共享事件。  
  
> [!NOTE]
>  您可以通过定义自定义事件来更改事件的默认行为。  对于自定义事件，`RaiseEvent` 语句调用事件的 `RaiseEvent` 访问器。  有关自定义事件的更多信息，请参见 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)。  
  
## 示例  
 下面的示例使用事件从 10 到 0 倒数秒。  这段代码阐释了几种与事件相关的方法、属性和语句，包括 `RaiseEvent` 语句。  
  
 引发事件的类是事件源，而处理事件的方法是事件处理程序。  事件源对它生成的事件可以具有多个处理程序。  当类引发事件时，将在每一个被选择用来处理该对象实例的事件的类上引发该事件。  
  
 本示例还使用一个窗体 \(`Form1`\)，该窗体具有一个按钮 \(`Button1`\) 和一个文本框 \(`TextBox1`\)。  单击此按钮时，第一个文本框从 10 到 0 秒进行倒计时。  全部时间（10 秒）过去后，第一个文本框显示“Done”（完成）。  
  
 `Form1` 的代码指定窗体的初始状态和最终状态。  它还包含引发事件时执行的代码。  
  
 若要使用此示例，请打开一个新的 Windows 应用程序项目，向主窗体 `Form1` 添加一个名为 `Button1` 的按钮和一个名为 `TextBox1` 的文本框。  然后右击窗体，并单击**“查看代码”**来打开代码编辑器。  
  
 将 `WithEvents` 变量添加到 `Form1` 类的声明部分。  
  
 [!code-vb[VbVbalrEvents#14](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_2.vb)]  
  
## 示例  
 将下面的代码添加到 `Form1` 的代码中。  替换可能存在的任何重复过程，如 `Form_Load` 或 `Button_Click`。  
  
 [!code-vb[VbVbalrEvents#15](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_3.vb)]  
  
 按 F5 键运行前面的示例，然后单击标有**“开始”**的按钮。  第一个文本框将开始倒计时读秒。  全部时间（10 秒）过去后，第一个文本框显示“Done”（完成）。  
  
> [!NOTE]
>  `My.Application.DoEvents` 方法不会完全像窗体那样处理事件。  若要允许窗体直接处理事件，可以使用多线程处理。  有关更多信息，请参见[线程](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 请参阅  
 [事件](../../../visual-basic/programming-guide/language-features/events/events.md)   
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [AddHandler 语句](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [RemoveHandler 语句](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)