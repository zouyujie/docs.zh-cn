---
title: "如何：在 Visual Basic 中调用事件处理程序 | Microsoft Docs"
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
  - "事件处理程序"
  - "事件处理程序, 调用"
  - "过程, 调用"
  - "过程, 事件处理程序"
  - "Visual Basic 代码, 过程"
ms.assetid: 72e18ef8-144e-40df-a1f4-066a57271e28
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：在 Visual Basic 中调用事件处理程序
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

“事件”是可被某程序组件识别的操作或事件（如鼠标单击或超出信用限额），可以为它编写响应代码。  “事件处理程序”是为响应事件而编写的代码。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的事件处理程序是一个 `Sub` 过程。  但是调用它的方法通常与调用其他 `Sub` 过程的方法不同。  相反，将此过程标识为事件的处理程序。  可以使用一个 [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md) 子句和一个 [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md) 变量，或一个 [AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md) 来执行此操作。  使用 `Handles` 子句是在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中声明事件处理程序的默认方式。  在集成开发环境 \(IDE\) 中编程时通过设计器编写事件处理程序便使用这种方式。  `AddHandler` 语句适用于在运行时动态引发事件。  
  
 事件发生时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 自动调用事件处理程序过程。  对此事件具有访问权限的任何代码都可以通过执行 [RaiseEvent 语句](../../../../visual-basic/language-reference/statements/raiseevent-statement.md) 引起此事件。  
  
 可以使多个事件处理程序与同一事件关联。  在某种情况下，可以取消处理程序与事件的关联。  有关更多信息，请参见 [事件](../../../../visual-basic/programming-guide/language-features/events/events.md)。  
  
### 使用 Handles 和 WithEvents 调用事件处理程序  
  
1.  请确保事件是以 [Event 语句](../../../../visual-basic/language-reference/statements/event-statement.md)声明的。  
  
2.  使用 [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md) 关键字在模块或类级别声明一个对象变量。  此变量的 `As` 子句必须指定引发此事件的类。  
  
3.  在负责事件处理的 `Sub` 过程的声明中，添加指定 `WithEvents` 变量和事件名称的 [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md) 子句。  
  
4.  事件发生时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 自动调用 `Sub` 过程。  代码可以使用 `RaiseEvent` 语句引发事件。  
  
     下面的示例定义一个事件和一个指向引用引发事件的类的 `WithEvents` 变量。  处理事件的 `Sub` 过程使用 `Handles` 子句指定它处理的类和事件。  
  
     [!code-vb[VbVbcnProcedures#4](./codesnippet/VisualBasic/how-to-call-an-event-handler_1.vb)]  
  
### 使用 AddHandler 调用事件处理程序  
  
1.  请确保事件是以 `Event` 语句声明的。  
  
2.  执行 [AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md)，以动态方式将处理事件的 `Sub` 过程连接到事件。  
  
3.  事件发生时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 自动调用 `Sub` 过程。  代码可以使用 `RaiseEvent` 语句引发事件。  
  
     下面的示例定义 `Sub` 过程以处理窗体的 <xref:System.Windows.Forms.Form.Closing> 事件。  它接着使用 [AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md) 与作为 <xref:System.Windows.Forms.Form.Closing> 的事件处理程序的 `catchClose` 过程关联。  
  
     [!code-vb[VbVbcnProcedures#5](./codesnippet/VisualBasic/how-to-call-an-event-handler_2.vb)]  
  
     可以通过执行 [RemoveHandler 语句](../../../../visual-basic/language-reference/statements/removehandler-statement.md) 取消事件处理程序与事件的关联。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [AddressOf 运算符](../../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [如何：创建过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure.md)   
 [如何：调用不返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-does-not-return-a-value.md)