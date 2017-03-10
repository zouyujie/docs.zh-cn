---
title: "宽松委托转换 (Visual Basic) | Microsoft Docs"
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
  - "转换, 松散委托"
  - "委托 [Visual Basic], 松散转换"
  - "松散委托转换 [Visual Basic]"
ms.assetid: 64f371d0-5416-4f65-b23b-adcbf556e81c
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 宽松委托转换 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过进行宽松委托转换，可以将 Sub 和函数分配给委托或处理程序，即使在签名不同时仍可如此。因此，委托绑定将与方法调用中已允许的绑定保持一致。  
  
## 参数和返回类型  
 为替代签名完全匹配，宽松转换要求在将 `Option Strict` 设置为 `On` 的时满足以下条件：  
  
-   必须存在从每个委托参数的数据类型到所分配函数或 `Sub` 的相应参数数据类型的扩大转换。  在下面的代码中，委托 `Del1` 具一个参数 `Integer`。  所分配的 lambda 表达式中的参数 `m` 必须具有一个数据类型（对于该数据类型，存在一个以 `Integer` 为转换来源的扩大转换），如 `Long` 或 `Double`。  
  
     [!code-vb[VbVbalrRelaxedDelegates#1](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#1)]  
  
     [!code-vb[VbVbalrRelaxedDelegates#2](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#2)]  
  
     仅当 `Option Strict` 设置为 `Off` 时，才允许进行收缩转换。  
  
     [!code-vb[VbVbalrRelaxedDelegates#8](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module2.vb#8)]  
  
-   反方向中必须存在从所分配函数或 `Sub` 的返回类型到委托的返回类型的扩大转换。  在下面的示例中，所分配的每个 lambda 表达式体的计算结果都必须是扩大到 `Integer` 的数据类型，因为 `del1` 的返回类型为 `Integer`。  
  
     [!code-vb[VbVbalrRelaxedDelegates#3](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#3)]  
  
 如果将 `Option Strict` 设置为 `Off`，则会在两个方向上移除扩大限制。  
  
 [!code-vb[VbVbalrRelaxedDelegates#4](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module2.vb#4)]  
  
## 忽略参数规范  
 宽松委托还允许完全忽略分配的方法中的参数规范：  
  
 [!code-vb[VbVbalrRelaxedDelegates#5](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#5)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#6](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#6)]  
  
 请注意，不能指定一些参数而忽略其他参数。  
  
 [!code-vb[VbVbalrRelaxedDelegates#15](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#15)]  
  
 忽略参数功能在涉及一些复杂参数的情况下（如定义事件处理程序）非常有用。  未使用某些事件处理程序的参数。  但处理程序可以直接访问注册事件的控件的状态，并忽略这些参数。  在不产生多义性时，宽松委托允许忽略此类声明中的参数。  在下面的示例中，可以将完全指定的方法 `OnClick` 重新编写为 `RelaxedOnClick`。  
  
```vb#  
Sub OnClick(ByVal sender As Object, ByVal e As EventArgs) Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
  
Sub RelaxedOnClick() Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
```  
  
## AddressOf 示例  
 在先前的示例中使用了 lambda 表达式，以便轻松地查看类型关系。  但是，对于使用 `AddressOf`、`Handles` 或 `AddHandler` 的委托分配，允许相同的宽松转换。  
  
 在下面的示例中，函数 `f1`、`f2`、`f3` 和 `f4` 都可以分配给 `Del1`。  
  
 [!code-vb[VbVbalrRelaxedDelegates#1](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#1)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#7](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#7)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#9](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#9)]  
  
 仅当 `Option Strict` 设置为 `Off` 时，下面的示例才是有效的。  
  
 [!code-vb[VbVbalrRelaxedDelegates#14](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module2.vb#14)]  
  
## 删除函数返回值  
 通过进行宽松委托转换，可以为 `Sub` 委托分配函数，并有效地忽略该函数的返回值。  但是，不能将 `Sub` 分配给函数委托。  在下面的示例中，将函数 `doubler` 的地址分配给 `Sub` 委托 `Del3`。  
  
 [!code-vb[VbVbalrRelaxedDelegates#10](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#10)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#11](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#11)]  
  
## 请参阅  
 [lambda 表达式](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [如何：在 Visual Basic 中将过程传递给另一过程](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)