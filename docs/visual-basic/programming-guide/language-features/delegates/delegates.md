---
title: "委托 (Visual Basic) | Microsoft Docs"
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
  - "委托 [Visual Basic]"
  - "Visual Basic 代码, 委托"
ms.assetid: 410b60dc-5e60-4ec0-bfae-426755a2ee28
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 委托 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

委托是引用方法的对象。  由于它们与其他编程语言中所使用的函数指针相似，因此它们有时也被称为*“类型安全的函数指针”*。  但与函数指针不同的是，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 委托是基于 <xref:System.Delegate?displayProperty=fullName> 类的引用类型。  委托可以引用共享方法（无需类的特定实例便可调用的方法）和实例方法。  
  
## 委托和事件  
 委托在调用过程和被调用过程需要媒介的情况下是很有用的。  例如，您可能想让一个引发事件的对象能够在不同的环境下调用不同的事件处理程序。  遗憾的是，引发事件的对象无法提前知道哪个事件处理程序正在处理特定事件。  通过在您使用 `AddHandler` 语句时为您创建委托，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 允许您动态地将事件处理程序与事件相关联。  在运行时，委托将各种调用转发到相应的事件处理程序。  
  
 虽然您可以创建自己的委托，但在大多数情况下，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 为您创建委托并保管详细信息。  例如，`Event` 语句将名为 `<EventName>EventHandler` 的委托类隐式定义为 `Event` 语句所在类的嵌套类，且其签字与该事件相同。  `AddressOf` 语句可隐式创建一个引用特定过程的委托的实例。  下面两行代码是等效的。  您会发现，第一行是显式创建 `Eventhandler` 的实例，该实例引用了作为参数发送的 `Button1_Click` 方法。  第二行以更加便捷的方法执行相同操作。  
  
 [!code-vb[VbVbalrDelegates#6](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/delegates_1.vb)]  
  
 只要编译器可以用上下文确定委托的类型，就可以使用速写方法创建委托。  
  
## 声明使用现有委托类型的事件  
 某些情况下，可能会要声明某事件使用现有委托类型为基础委托。  以下语法说明了进行声明的方式：  
  
 [!code-vb[VbVbalrDelegates#7](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/delegates_2.vb)]  
  
 该语法在将多个事件路由到同一处理程序时是很有用的。  
  
## 委托变量和参数  
 可以将委托用于其他非事件相关任务（如自由线程处理），或用于运行时需调用不同函数版本的过程。  
  
 例如，假设您有一个分类广告应用程序，其中包含一个汽车名称列表框。  广告按标题进行排序，这些标题则通常都是汽车的品牌。  某些汽车的名称所含年份早于该品牌出现的年份时您就会遇到问题。  问题在于列表框内置的排序功能只使用字符代码排序；它将以日期开头的广告放在前面，后面是以品牌开头的广告。  
  
 若要解决这一问题，可以在某个类中创建一个排序过程，该类在多数列表框中使用标准字母排序，但是它可以在运行时切换为汽车广告的自定义排序。  要达到这一目的，可以使用委托在运行时将自定义排序过程传递给排序类。  
  
## AddressOf 和 Lambda 表达式  
 每个委托类都定义一个被传递对象方法规范的构造函数。  委托构造函数的参数必须是对方法或 lambda 表达式的引用。  
  
 若要指定对方法的引用，请使用下面的语法：  
  
 `AddressOf` \[`expression`.\]`methodName`  
  
 `expression` 的编译时类型必须是类或接口的名称，而该类或接口包含签名与委托类的签名相匹配的指定名称的方法。  `methodName` 可以是共享方法，也可以是实例方法。  即使为类的默认方法创建了委托，`methodName` 也不是可选项。  
  
 若要指定 lambda 表达式，请使用下面的语法：  
  
 `Function` \(\[`parm` As `type`, `parm2` As `type2`, ...\]\) `expression`  
  
 以下示例显示了用于为委托指定引用的 `AddressOf` 和 lambda 表达式。  
  
 [!code-vb[VbVbalrDelegates#15](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/delegates_3.vb)]  
  
 函数的签名必须与委托类型的签名相匹配。  有关 lambda 表达式的更多信息，请参见 [lambda 表达式](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  有关为委托分配 lambda 表达式和 `AddressOf` 的更多示例，请参见[宽松委托转换](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。  
  
## 相关主题  
  
|标题|说明|  
|--------|--------|  
|[如何：调用委托方法](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)|提供一个示例，该示例演示如何将方法与委托关联，然后通过委托调用该方法。|  
|[如何：在 Visual Basic 中将过程传递给另一过程](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)|演示如何使用委托将一个过程传递到另一个过程。|  
|[宽松委托转换](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)|描述如何将 Sub 和函数分配给委托或处理程序（即使在其签名不相同时）。|  
|[事件](../../../../visual-basic/programming-guide/language-features/events/events.md)|提供对 Visual Basic 中的事件的概述。|