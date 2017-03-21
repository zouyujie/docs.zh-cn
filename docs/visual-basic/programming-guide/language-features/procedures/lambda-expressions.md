---
title: "Lambda 表达式 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.LambdaFunction"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "表达式 [Visual Basic], lambda"
  - "函数 [Visual Basic], Lambda 表达式"
  - "内联函数 [Visual Basic]"
  - "lambda 表达式 [Visual Basic]"
ms.assetid: 137064b0-3928-4bfa-ba71-c3f9cbd951e2
caps.latest.revision: 52
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 52
---
# Lambda 表达式 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

“Lambda 表达式”是一种没有名称的函数或子例程，可在委托有效的任何地方使用。  Lambda 表达式可以是函数或子例程，且可为单行或多行。  可以将值从当前范围传递到 Lambda 表达式。  
  
> [!NOTE]
>  `RemoveHandler` 语句是一个例外。  不能为 `RemoveHandler` 的委托参数传递 lambda 表达式。  
  
 使用 `Function` 或 `Sub` 关键字可以创建 Lambda 表达式，就像创建标准函数或子例程一样。  但是，Lambda 表达式包括在语句中。  
  
 下面的示例是一个 lambda 表达式，该表达式递增其参数并返回值。  该示例同时显示了一个函数的单行和多行 Lambda 表达式语法。  
  
 [!code-vb[VbVbalrLambdas#14](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_1.vb)]  
  
 下面的示例是将值写入控制台的 Lambda 表达式。  该示例同时显示了一个子例程的单行和多行 Lambda 表达式语法。  
  
 [!code-vb[VbVbalrLambdas#15](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_2.vb)]  
  
 请注意，在前面的示例中，为一个变量名称分配了 Lambda 表达式。  只要引用该变量，就会调用 Lambda 表达式。  还可以同时声明和调用 Lambda 表达式，如下面的示例所示。  
  
 [!code-vb[VbVbalrLambdas#3](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_3.vb)]  
  
 Lambda 表达式可以作为函数调用的值返回（如本主题后面[上下文](#context)部分中的示例所示），或作为实参传递给会获取委托类型的形参，如下面的示例所示。  
  
 [!code-vb[VbVbalrLambdas#8](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_4.vb)]  
  
## Lambda 表达式语法  
 Lambda 表达式的语法类似于标准函数或子例程的语法。  区别如下：  
  
-   lambda 表达式没有名称。  
  
-   Lambda 表达式不能有修饰符，例如 `Overloads` 或 `Overrides`。  
  
-   单行 Lambda 函数不使用 `As` 子句来指定返回类型。  相反，类型是从 lambda 表达式主体计算得出的值推断而来的。  例如，如果 lambda 表达式的主体为 `cust.City = "London"`，则其返回类型为 `Boolean`。  
  
-   在多行 Lambda 函数中，可以使用 `As` 子句指定返回类型，或者省略 `As` 子句以便推断返回类型。  省略某多行 Lambda 函数的 `As` 子句时，返回类型被推断为该多行 Lambda 函数中所有 `Return` 语句的主导类型。  *主导类型*是唯一可以扩大到的所有其他类型的类型。  如果无法确定此唯一类型，则主导类型是数组中所有其他类型都可以收缩到的唯一类型。  如果这两种唯一类型都无法确定，则主导类型是 `Object`。  在这种情况下，如果 `Option Strict` 设置为 `On`，则会发生编译器错误。  
  
     例如，如果表达式提供给`Return`语句包含值类型的`Integer`， `Long`，和`Double`，则生成的数组类型不`Double`。  `Integer` 和 `Long` 都扩大到 `Double` 且仅扩大到 `Double`。  因此，`Double` 是主导类型。  有关更多信息，请参见[扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
-   单行函数的主体必须是返回一个值的表达式，而不是语句。  单行函数没有 `Return` 语句。  单行函数返回的值是函数主体中的表达式的值。  
  
-   单行子例程的主体必须是单行语句。  
  
-   单行函数和子例程不包括 `End Function` 或 `End Sub` 语句。  
  
-   可以使用 `As` 关键字指定 Lambda 表达式参数的数据类型，也可以推断参数的数据类型。  要么所有参数都必须具有指定的数据类型，要么必须推断所有类型。  
  
-   不允许使用 `Optional` 和 `Paramarray` 参数。  
  
-   不允许使用泛型参数。  
  
## 异步 Lambda  
 您可以轻松地创建的 lambda 表达式或语句使用合并异步处理的[Async](../../../../visual-basic/language-reference/modifiers/async.md)和[Await 运算符](../../../../visual-basic/language-reference/operators/await-operator.md)关键字。  例如，下面的 Windows 窗体示例包含一个事件处理程序调用，并等待异步方法， `ExampleMethodAsync`。  
  
```vb  
Public Class Form1  
  
    Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' ExampleMethodAsync returns a Task.  
        Await ExampleMethodAsync()  
        TextBox1.Text = vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Async Function ExampleMethodAsync() As Task  
        ' The following line simulates a task-returning asynchronous process.  
        Await Task.Delay(1000)  
    End Function  
  
End Class  
  
```  
  
 您可以通过使用在异步 lambda 添加相同的事件处理程序[AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md)。  若要将此处理程序，添加`Async`之前的 lambda 参数列表，如以下示例所示的修饰符。  
  
```vb  
Public Class Form1  
  
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load  
        AddHandler Button1.Click,   
            Async Sub(sender1, e1)  
                ' ExampleMethodAsync returns a Task.  
                Await ExampleMethodAsync()  
                TextBox1.Text = vbCrLf & "Control returned to Button1_ Click."  
            End Sub  
    End Sub  
  
    Async Function ExampleMethodAsync() As Task  
        ' The following line simulates a task-returning asynchronous process.  
        Await Task.Delay(1000)  
    End Function  
  
End Class  
  
```  
  
 有关如何创建和使用异步方法的详细信息，请参阅[使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)。  
  
##  <a name="context"></a> 上下文  
 Lambda 表达式与它被定义时所在的范围共享其上下文。  它与在包含范围中编写的任何代码具有相同的访问权限。  这包括访问包含范围中的成员变量、函数和子函数、`Me` 以及参数和局部变量的权限。  
  
 对包含范围中的局部变量和参数的访问可以超出该范围的生存期。  只要引用 lambda 表达式的委托不能进行垃圾回收，就将保留对原始环境中的变量的访问。  在下面的示例中，变量 `target` 对于 `makeTheGame` 方法（lambda 表达式 `playTheGame` 在该方法中定义）是局部变量。  请注意，返回并分配给 `Main` 中 `takeAGuess` 的 lambda 表达式仍然具有访问局部变量 `target` 的权限。  
  
 [!code-vb[VbVbalrLambdas#12](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_5.vb)]  
  
 下面的示例演示嵌套 lambda 表达式所具有的宽广的访问权限范围。  在 `Main` 中将返回的 lambda 表达式作为 `aDel` 执行时，该表达式能够访问下列元素：  
  
-   在其中定义该表达式的类的字段：`aField`  
  
-   在其中定义该表达式的类的属性：`aProp`  
  
-   在其中定义该表达式的方法 `functionWithNestedLambda` 的参数：`level1`  
  
-   `functionWithNestedLambda` 的局部变量：`localVar`  
  
-   在其中嵌套该表达式的 lambda 表达式的参数：`level2`  
  
 [!code-vb[VbVbalrLambdas#9](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_6.vb)]  
  
## 转换为委托类型  
 可以将 lambda 表达式隐式转换为兼容的委托类型。  有关兼容性的一般要求的信息，请参见[宽松委托转换](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。  例如，下面的代码示例演示一个隐式转换为 `Func(Of Integer, Boolean)` 或匹配委托签名的 Lambda 表达式。  
  
 [!code-vb[VbVbalrLambdas#16](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_7.vb)]  
  
 下面的代码示例演示一个隐式转换为 `Sub(Of Double, String, Double)` 或匹配委托签名的 Lambda 表达式。  
  
 [!code-vb[VbVbalrLambdas#23](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_8.vb)]  
  
 在将 Lambda 表达式分配给委托或将其作为实参传递到过程时，可以指定形参名称，但请省略其数据类型，以便从委托中获取类型。  
  
## 示例  
  
-   下面的示例定义了一个 lambda 表达式，如果可以为 null 的参数已被赋值，则该表达式返回 `True`；如果该参数的值为 `Nothing`，则返回 `False`。  
  
     [!code-vb[VbVbalrLambdas#4](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_9.vb)]  
  
-   下面的示例定义了一个 lambda 表达式，该表达式返回数组中最后一个元素的索引。  
  
     [!code-vb[VbVbalrLambdas#5](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_10.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [可以为 Null 的值类型](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [如何：在 Visual Basic 中将过程传递给另一过程](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [如何：创建 lambda 表达式](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-lambda-expression.md)   
 [宽松委托转换](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)