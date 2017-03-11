---
title: "Try...Catch...Finally 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Try...Catch...Finally"
  - "vb.when"
  - "vb.Finally"
  - "vb.Catch"
  - "vb.Try"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Catch 语句"
  - "错误处理, 在运行代码时"
  - "Finally 关键字 [Visual Basic], Try...Catch...Finally"
  - "结构化异常处理, Try...Catch...Finally 语句"
  - "Try 语句"
  - "Try 语句, Try...Catch...Finally"
  - "Try...Catch...Finally 语句"
  - "try-catch 异常处理, Try...Catch...Finally 语句"
  - "Visual Basic 代码, 在运行时处理错误"
  - "When 关键字"
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
caps.latest.revision: 69
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 69
---
# Try...Catch...Finally 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

用于处理给定代码段中可能出现的某些或所有错误，而同时代码仍保持运行。  
  
## 语法  
  
```  
Try  
    [ tryStatements ]  
    [ Exit Try ]  
[ Catch [ exception [ As type ] ] [ When expression ]  
    [ catchStatements ]  
    [ Exit Try ] ]  
[ Catch ... ]  
[ Finally  
    [ finallyStatements ] ]  
End Try  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`tryStatements`|可选。  可能发生错误的语句。  可以是复合语句。|  
|`Catch`|可选。  允许使用多个 `Catch` 块。  如果在处理 `Try` 块时发生异常，则会按文本顺序检查每条 `Catch` 语句，以确定它是否处理异常，`exception` 代表已引发的异常。|  
|`exception`|可选。  任何变量名称。  `exception` 的初始值是引发的错误的值。  它将与 `Catch` 一起使用以指定所捕获的错误。  如果省略，则 `Catch` 语句将捕获所有异常。|  
|`type`|可选。  指定类筛选器的类型。  如果 `exception` 的值采用的是 `type` 所指定的类型或者派生类型，则该标识符将绑定到异常对象。|  
|`When`|可选。  带有 `When` 子句的 `Catch` 语句只会在 `expression` 的计算结果为 `True` 时捕获异常。  `When` 子句仅在检查异常类型之后应用，`expression` 可以引用表示异常的标识符。|  
|`expression`|可选。  必须可隐式转换为 `Boolean`。  说明一般筛选器的任何表达式。  通常用来根据错误号进行筛选。  它与 `When` 关键字一同使用，以指定捕获错误时的环境。|  
|`catchStatements`|可选。  用于处理在关联的 `Try` 中发生的错误的语句。  可以是复合语句。|  
|`Exit Try`|可选。  用于退出 `Try...Catch...Finally` 结构的关键字。  将继续执行紧跟在 `End Try` 语句后面的代码。  `Finally` 语句仍将被执行。  不允许在 `Finally` 块中使用。|  
|`Finally`|可选。  当执行过程离开 `Try...Catch` 语句的任何部分时，总是会执行 `Finally` 块。|  
|`finallyStatements`|可选。  在所有其他错误处理结束后执行的语句。|  
|`End Try`|终止 `Try...Catch...Finally` 结构。|  
  
## 备注  
 如果预计特定代码部分会发生特定异常，请将该代码放到 `Try` 块中，并使用一个 `Catch` 块来保留控制焦点，如果发生异常则对其进行处理。  
  
 `Try…Catch` 语句由一个 `Try` 块后跟一个或多个 `Catch` 子句构成，这些子句指定各种异常处理的程序。  如果 `Try` 块中引发异常，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将查找处理异常的 `Catch` 语句。  如果未找到匹配的 `Catch` 语句，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会检查调用当前方法的方法，然后会遍历调用堆栈。  如果找不到 `Catch` 块，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会向用户显示一条有关未经处理的异常的消息并停止执行程序。  
  
 可以在 `Try…Catch` 语句中使用多个 `Catch` 语句。  如果执行此操作，则 `Catch` 子句的顺序很重要，因为会按顺序检查它们。  将先捕获特定程度较高的异常，而不是特定程度较小的异常。  
  
 下面的 `Catch` 语句条件是最不特定的，将捕获从 <xref:System.Exception> 类派生的所有异常。  在捕获所有预期的特定异常之后，通常应将其中一个变量用作 `Try...Catch...Finally` 结构中的最后一个 `Catch` 块。  控制流绝不会到达遵循以下任一变化的 `Catch` 块。  
  
-   `type` 为 `Exception`，例如：`Catch ex As Exception`  
  
-   语句不包括 `exception` 变量，例如： `Catch`  
  
 当 `Try…Catch…Finally` 语句嵌套在另一个 `Try` 块中时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 首先检查最里面 `Try` 块中的每个 `Catch` 语句。  如果没有找到匹配的 `Catch` 语句，则继续搜索外部 `Try…Catch…Finally` 块的 `Catch` 语句。  
  
 `Try` 块中的局部变量将无法在 `Catch` 块中使用，因为它们是独立的块。  如果要在多个块中使用某个变量，请在 `Try...Catch...Finally` 结构之外声明该变量。  
  
> [!TIP]
>  `Try…Catch…Finally` 语句可用作 IntelliSense 代码段。  在代码段管理器中，展开**“代码模式 \- 如果，对于每一个，尝试捕获，属性，等等”**，然后展开**“错误处理\(异常\)”**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
## Finally 块  
 如果在退出 `Try` 结构之前必须运行一个或多个语句，则可以使用 `Finally` 块。  控制权在即将传递到 `Try…Catch` 结构外之前，将传递到 `Finally` 块。  即使在 `Try` 结构内部的任何位置发生异常也是这样。  
  
 `Finally` 块可用于运行即使有例外也必须执行的任何代码。  将控制权传递给 `Finally` 块，与 `Try...Catch` 块的退出方式无关。  
  
 `Finally` 块中的代码将运行，即使在 `Try` 或 `Catch` 块中遇到 `Return` 语句。  在以下情况中控制权不会从 `Try` 或 `Catch` 块传递到相应的 `Finally` 块：  
  
-   在 `Try` 或 `Catch` 块中遇到 [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)。  
  
-   在 `Try` 或 `Catch` 块中引发了 <xref:System.StackOverflowException>。  
  
 它是无效的显式调用执行到 `Finally` 块。  在 `Finally` 外部的调用执行块是无效的，除非将异常。  
  
 如果 `Try` 语句不包含至少一个 `Catch` 块，它必须包含 `Finally` 块。  
  
> [!TIP]
>  如果不需要捕捉特定异常，则 `Using` 语句的行为与 `Try…Finally` 块一样，且无论以何种方式退出块，都保证会处置资源。  发有未经处理的异常，也是如此。  有关更多信息，请参见 [Using 语句](../../../visual-basic/language-reference/statements/using-statement.md)。  
  
## 异常参数  
 `Catch` 块 `exception` 参数是 <xref:System.Exception> 类或派生自 `Exception` 类的类的实例。  `Exception` 类实例与 `Try` 块中发生的错误相对应。  
  
 `Exception` 对象的属性可帮助您确定异常的原因和位置。  例如，<xref:System.Exception.StackTrace%2A> 属性列出导致异常的被调用方法，帮助您找到错误在代码中发生的位置。  <xref:System.Exception.Message%2A> 返回一条描述异常的消息。  <xref:System.Exception.HelpLink%2A> 返回指向关联的帮助文件的链接。  <xref:System.Exception.InnerException%2A> 返回引发当前异常的 `Exception` 对象，或如果没有原始 `Exception`，返回 `Nothing`。  
  
## 使用 Try…Catch 语句时的注意事项  
 使用 `Try…Catch` 语句只在发生不寻常或意外的程序事件时发送信号。  发生这种情况的原因包括如下方面：  
  
-   在运行时捕捉异常会产生额外的开销，并且可能比预检查慢以避免异常。  
  
-   如果未正确处理 `Catch` 块，则异常可能不会正确报告给用户。  
  
-   异常处理会使程序更加复杂。  
  
 你并不总是需要 `Try…Catch` 语句，以检查有可能出现的条件。  下面的示例在尝试打开文件之前，检查该文件是否存在。  这会减少捕获 <xref:System.IO.File.OpenText%2A> 方法所引发异常的需要。  
  
 [!code-vb[VbVbalrStatements#94](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/try-catch-finally-statem_1.vb)]  
  
 确保 `Catch` 块中的代码可以将异常正确报告给用户，无论通过线程安全日志记录还是相应的消息。  否则，异常可能仍是未知的。  
  
## 异步方案  
 如果标记与 [Async](../../../visual-basic/language-reference/modifiers/async.md) 修饰符的方法，在方法可以使用 [等待](../../../visual-basic/language-reference/operators/await-operator.md) 运算符。  与 `Await` 运算符的语句挂起方法的执行，直到等待任务完成。  任务表示正在进行的工作。  在与 `Await` 运算符时的任务完成，执行在同一方法还原。  有关更多信息，请参见 [异步程序中的控制流](../Topic/Control%20Flow%20in%20Async%20Programs%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 异步方法返回的任务处于错误状态可能会关闭，指示已完成由于未经处理的异常。  任务在一个已取消状态也可以关闭，将导致引发在等待表达式外部的 `OperationCanceledException`。  捕获异常的任何一种类型，将与 `Try` 的任务被阻止，并捕获在 `Catch` 的异常块的 `Await` 表达式。  示例本主题后面提供。  
  
 因为多个异常为其出错，负责任务可以在已出错状态。  例如，任务可能为调用的结果。<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>。  当您等待此类任务时，捕获的异常仅有一个异常，因此，您无法预测哪个异常将捕获。  示例本主题后面提供。  
  
 `Await` 表达式不能在 `Catch` 块或 `Finally` 块。  
  
## 迭代器  
 迭代器函数或 `Get` 访问器对集合的自定义迭代。  迭代器使用一个 [Yield](../../../visual-basic/language-reference/statements/yield-statement.md) 语句返回集合中的每个元素一个节点。  使用 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)，则调用迭代器函数。  
  
 `Yield` 语句将在 `Try` 块。  `Try` 块包含一个 `Yield` 语句可以具有 `Catch` 块，并可以具有 `Finally` 块。  请参见 [迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md) “尝试在Visual Basic块”一节的示例。  
  
 `Yield` 语句不能在 `Catch` 块或 `Finally` 块。  
  
 如果 `For Each` 主体\(在迭代器函数之外\)引发异常，`Catch` 在迭代器功能块，不会执行，但 `Finally` 在迭代器功能块中执行。  `Catch` 块在迭代器功能出现在迭代器函数内仅捕获的异常中。  
  
## 部分信任的情形  
 在部分信任的情况下（如网络共享上承载的应用程序），`Try...Catch...Finally` 将不会捕获在调用包含该调用的方法之前发生的安全异常。  当将下面的示例放置在服务器共享上并从此处运行时，将生成错误“System.Security.SecurityException: 请求失败”。有关安全异常的更多信息，请参见 <xref:System.Security.SecurityException> 类。  
  
 [!code-vb[VbVbalrStatements#85](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/try-catch-finally-statem_2.vb)]  
  
 在这种部分信任的情况下，您必须将 `Process.Start` 语句放在单独的 `Sub` 中。  对 `Sub` 的初次调用将失败。  这使得 `Try...Catch` 能够在包含 `Process.Start` 的 `Sub` 启动并产生安全异常之前捕获它。  
  
## 示例  
 下面的示例阐释了 `Try...Catch...Finally` 语句的结构。  
  
 [!code-vb[VbVbalrStatements#86](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/try-catch-finally-statem_3.vb)]  
  
## 示例  
 下面的示例演示中，`CreateException` 方法引发 `NullReferenceException`。  代码生成的异常不在 `Try` 数据块中.  因此，`CreateException` 方法不对异常进行处理。  `RunSample` 方法未处理该异常，因为对 `CreateException` 方法的调用是在 `Try` 中。  
  
 对于若干类型的异常，该示例包含 `Catch` 语句，排列顺序是从最特定到最一般。  
  
 [!code-vb[VbVbalrStatements#91](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/try-catch-finally-statem_4.vb)]  
  
## 示例  
 下面示例显示如何使用 `Catch When` 语句筛选条件表达式。  如果条件表达式计算为 `True`，则 `Catch` 块中的代码将运行。  
  
 [!code-vb[VbVbalrStatements#92](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/try-catch-finally-statem_5.vb)]  
  
## 示例  
 下面的示例有 `Try…Catch` 语句，该语句包含在 `Try` 块中。  内部 `Catch` 块引发异常，该异常的 `InnerException` 属性设置为原始异常。  外部 `Catch` 块报告自己的异常和内部异常。  
  
 [!code-vb[VbVbalrStatements#93](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/try-catch-finally-statem_6.vb)]  
  
## 示例  
 下面的示例演示异常处理异步方法的。  若要捕获适用于异步任务中的异常，`Await` 表达式。`Try` 块调用方，因此，异常。`Catch` 捕获块。  
  
 取消对演示异常处理的示例中的 `Throw New Exception` 行。  异常在 `Catch` 捕获块，任务的 `IsFaulted` 属性设置为 `True`，并且，任务的 `Exception.InnerException` 属性设置为异常。  
  
 取消注释演示时所发生的 `Throw New OperationCancelledException` 行，则取消异步处理。  异常在 `Catch` 捕获块，并且，任务的 `IsCanceled` 属性设置为 `True`。  在某些条件下但是，这不适用于此示例，`IsFaulted` 设置为 `True`，并 `IsCanceled` 设置为 `False`。  
  
 [!code-vb[csAsyncExceptions#1](../../../csharp/language-reference/keywords/codesnippet/visualbasic/try-catch-finally-statem_7.vb)]  
  
## 示例  
 下面的示例演示异常处理多个任务可能导致多个异常的位置。  `Try` 块有 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> 返回的任务的 `Await` 表达式。  任务已完成，当 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> 当应用时的三个任务完成。  
  
 三个任务原因中的每一个异常。  `Catch` 块通过异常重复，任务中的 `Exception.InnerExceptions` 属性中找到 `Task.WhenAll` 返回。  
  
 [!code-vb[csAsyncExceptions#3](../../../csharp/language-reference/keywords/codesnippet/visualbasic/try-catch-finally-statem_8.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:System.Exception>   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [On Error 语句](../../../visual-basic/language-reference/statements/on-error-statement.md)   
 [有关使用代码段的最佳做法](/visual-studio/ide/best-practices-for-using-code-snippets)   
 [异常处理](../Topic/Exception%20Handling%20\(Task%20Parallel%20Library\).md)   
 [Throw 语句](../../../visual-basic/language-reference/statements/throw-statement.md)