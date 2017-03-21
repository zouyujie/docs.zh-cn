---
title: "如何：创建 Lambda 表达式 (Visual Basic) | Microsoft Docs"
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
  - "表达式 [Visual Basic], lambda"
  - "lambda 表达式 [Visual Basic]"
ms.assetid: 3279bd5c-80f7-410a-a7ba-f7085ed36aa5
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# 如何：创建 Lambda 表达式 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

lambda 表达式是没有名称的函数或子例程。  lambda 表达式可在委托类型有效的任何地方使用。  
  
### 创建单行 lambda 表达式函数  
  
1.  在任何可以使用委托类型的情况下，键入关键字 `Function`，如下面的示例所示：  
  
     `Dim add1 =`   `Function`  
  
2.  在紧跟在 `Function` 后面的括号中键入函数的参数。  请注意，不要在 `Function` 后面指定名称。  
  
     `Dim add1 = Function`   `(num As Integer)`  
  
3.  在参数列表后面，键入单个表达式作为函数体。  该表达式计算得出的值即为函数返回的值。  不要使用 `As` 子句指定返回类型。  
  
     [!code-vb[VbVbalrLambdas#1](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_1.vb)]  
  
     可以通过传递整数参数来调用 lambda 表达式。  
  
     [!code-vb[VbVbalrLambdas#2](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_2.vb)]  
  
4.  或者，也可以按下面的示例所示得到同样的结果：  
  
     [!code-vb[VbVbalrLambdas#3](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_3.vb)]  
  
### 创建单行 lambda 表达式子例程  
  
1.  在任何可以使用委托类型的情况下，键入关键字 `Sub`，如下面的示例所示。  
  
     `Dim add1 =`   `Sub`  
  
2.  在紧跟在 `Sub` 后面的括号中键入子例程的参数。  请注意，不要在 `Sub` 后面指定名称。  
  
     `Dim add1 = Sub`   `(msg As String)`  
  
3.  在参数列表后面，键入单个语句作为子例程体。  
  
     [!code-vb[VbVbalrLambdas#17](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_4.vb)]  
  
     可以通过传递字符串参数来调用 lambda 表达式。  
  
     [!code-vb[VbVbalrLambdas#18](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_5.vb)]  
  
### 创建多行 lambda 表达式函数  
  
1.  在任何可以使用委托类型的情况下，键入关键字 `Function`，如下面的示例所示。  
  
     `Dim add1 =`   `Function`  
  
2.  在紧跟在 `Function` 后面的括号中键入函数的参数。  请注意，不要在 `Function` 后面指定名称。  
  
     `Dim add1 = Function`   `(index As Integer)`  
  
3.  按 Enter。  将自动添加 `End Function` 语句。  
  
4.  在函数体内，添加以下代码以创建表达式并返回值。  不要使用 `As` 子句指定返回类型。  
  
     [!code-vb[VbVbalrLambdas#19](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_6.vb)]  
  
     可以通过传递整数参数来调用 lambda 表达式。  
  
     [!code-vb[VbVbalrLambdas#20](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_7.vb)]  
  
### 创建多行 lambda 表达式子例程  
  
1.  在任何可以使用委托类型的情况下，键入关键字 `Sub`，如下面的示例所示：  
  
     `Dim add1 =`   `Sub`  
  
2.  在紧跟在 `Sub` 后面的括号中键入子例程的参数。  请注意，不要在 `Sub` 后面指定名称。  
  
     `Dim add1 = Sub`  `(msg As String)`  
  
3.  按 Enter。  将自动添加 `End Sub` 语句。  
  
4.  在函数体内，添加以下代码以在调用子例程时执行。  
  
     [!code-vb[VbVbalrLambdas#21](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_8.vb)]  
  
     可以通过传递字符串参数来调用 lambda 表达式。  
  
     [!code-vb[VbVbalrLambdas#22](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_9.vb)]  
  
## 示例  
 lambda 表达式的一个常见用途是定义一个函数，该函数可作为 `Delegate` 类型的形参的实参进行传递。  在下面的示例中，<xref:System.Diagnostics.Process.GetProcesses%2A> 方法返回在本地计算机上运行的进程的数组。  <xref:System.Linq.Enumerable> 类中的 <xref:System.Linq.Enumerable.Where%2A> 方法需要使用一个 `Boolean` 委托作为参数。  该示例中的 lambda 表达式就是为此目的而使用的。  对于每个仅有一个线程的进程以及在 `filteredList` 中选择的进程，它将返回 `True`。  
  
 [!code-vb[VbVbalrLambdas#10](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_10.vb)]  
  
 上一个示例等效于下面用[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext-md.md)] 语法编写的代码：  
  
 [!code-vb[VbVbalrLambdas#11](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_11.vb)]  
  
## 请参阅  
 <xref:System.Linq.Enumerable>   
 [lambda 表达式](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [如何：在 Visual Basic 中将过程传递给另一过程](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [Delegate 语句](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)