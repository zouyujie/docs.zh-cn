---
title: "使用字符串名调用属性或方法 (Visual Basic) | Microsoft Docs"
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
  - "CallByName 函数"
  - "调用方法, 字符串名称"
  - "方法调用, 字符串"
  - "方法 [Visual Basic], 使用字符串名称调用"
  - "对象 [Visual Basic], 设置属性"
  - "传递运算符"
  - "属性 [Visual Basic], 在运行时设置"
  - "设置属性, 在运行时设置对象属性"
  - "字符串 [Visual Basic], 将 new 运算符传递为"
ms.assetid: 79a7b8b4-b8c7-4ad8-aca8-12a9a2b32f03
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 使用字符串名调用属性或方法 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在大多数情况下，可以在设计时发现对象的属性和方法，然后编写处理它们的代码。  然而，在某些情况下，可能事先并不知道对象的属性和方法，也可能只是需要一些灵活性，使最终用户可以在运行时指定属性或执行方法。  
  
## CallByName 函数  
 例如，有这样一个客户端应用程序，它通过将运算符传递给 COM 组件来计算用户输入的表达式。  假设您经常向需要新运算符的组件添加新函数。  若使用标准对象访问技术，则在该客户端应用程序可以使用新运算符之前，必须对其进行重新编译和重新发布。  为避免这种情况，可以使用 `CallByName` 函数将新运算符作为字符串来传递，而不用更改应用程序。  
  
 `CallByName` 函数允许在运行时使用字符串指定属性或方法。  `CallByName` 函数的签名如下所示：  
  
 *Result* \= `CallByName`\(*Object*, *ProcedureName*, *CallType*, *Arguments*\(\)\)  
  
 第一个参数 *Object* 指您要操作的对象的名称。  *ProcedureName* 参数是一个包含要调用的方法名或属性过程名的字符串。  *CallType* 参数是一个常量，表示要调用的过程的类型：方法 \(`Microsoft.VisualBasic.CallType.Method`\)、属性读取 \(`Microsoft.VisualBasic.CallType.Get`\) 或属性设置 \(`Microsoft.VisualBasic.CallType.Set`\)。  参数 *Arguments* 是可选的，为包含过程的所有参数的 `Object` 类型数组。  
  
 `CallByName` 可在当前解决方案中与类一起使用，但它通常用于访问 COM 对象或 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] 程序集中的对象。  
  
 假定您将一个引用添加到一个包含名为 `MathClass` 的类的程序集中，其中这个类有几个名为 `SquareRoot` 的函数，如以下代码所示：  
  
 [!code-vb[VbVbalrOOP#53](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#53)]  
  
 您的应用程序可以使用文本框控件来控制将要调用的方法及其参数。  例如，如果 `TextBox1` 包含要计算的表达式，并且 `TextBox2` 用于输入函数名时，可以使用以下代码来调用 `TextBox1` 中表达式的 `SquareRoot` 函数：  
  
 [!code-vb[VbVbalrOOP#54](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#54)]  
  
 如果在 `TextBox1` 中输入“64”，在 `TextBox2` 中输入“SquareRoot”，然后调用 `CallMath` 过程，则将计算 `TextBox1` 中数字的平方根。  示例中的代码调用 `SquareRoot` 函数（它必须有一个字符串参数，该字符串包含要计算的表达式）并将“8”（64 的平方根）返回到 `TextBox1` 中。  当然，如果用户在 `TextBox2` 中输入无效字符串，字符串包含的是属性名而非方法名，或者方法中含附加的必选参数，则会发生运行时错误。  使用 `CallByName` 时必须添加可靠的错误处理代码，以便对这样的错误或其他错误预做防范。  
  
> [!NOTE]
>  `CallByName` 函数在某些情况下可能很有用，但您必须在其用处和其带来的性能影响之间进行权衡，因为使用 `CallByName` 调用过程在速度上比后期绑定调用稍慢一些。  如果所调用的函数像在循环内部那样被重复调用，`CallByName` 会对性能产生严重影响。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Interaction.CallByName%2A>   
 [确定对象类型](../../../../visual-basic/programming-guide/language-features/early-late-binding/determining-object-type.md)