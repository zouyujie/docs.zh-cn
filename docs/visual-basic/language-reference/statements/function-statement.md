---
title: "Function 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Function"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "创建的过程"
  - "Function 过程，Function 语句语法"
  - "函数 [Visual Basic]，function 过程"
  - "ParamArray 关键字，Function 语句"
  - "Private 关键字，Function 语句"
  - "声明过程"
  - "过程声明"
  - "Public 关键字，在 Function 语句"
  - "ByVal 关键字，Function 语句"
  - "递归过程"
  - "Implements 关键字，Function 语句"
  - "过程，返回值"
  - "Exit 语句，在 Function 过程"
  - "递归过程"
  - "As 关键字，在 Function 语句"
  - "可选关键字，Function 语句"
  - "Function 语句"
  - "Visual Basic 代码，Function 过程"
  - "过程、 函数"
  - "ByRef 关键字，Function 语句"
  - "Friend 关键字，Function 语句"
  - "End 关键字，Function 语句"
  - "Handles 关键字，Function 语句"
ms.assetid: a4497077-0f46-4ede-a27f-9e8670df52b9
caps.latest.revision: 62
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 62
---
# Function 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明名称、 参数和定义的代码 `Function` 过程。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async | Iterator ]  
Function name [ (Of typeparamlist) ] [ (parameterlist) ] [ As returntype ] [ Implements implementslist | Handles eventlist ]  
    [ statements ]  
    [ Exit Function ]  
    [ statements ]  
End Function  
```  
  
## <a name="parts"></a>部件  
  
-   `attributelist`  
  
     可选。 请参阅 [属性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
-   `accessmodifier`  
  
     可选。 可以是以下各项之一：  
  
    -   [公共](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [受保护](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [友元](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [专用](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     请参阅 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
-   `proceduremodifiers`  
  
     可选。 可以是以下各项之一：  
  
    -   [重载](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
    -   [重写](../../../visual-basic/language-reference/modifiers/overrides.md)  
  
    -   [可重写](../../../visual-basic/language-reference/modifiers/overridable.md)  
  
    -   [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
  
    -   [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
  
    -   `MustOverride Overrides`  
  
    -   `NotOverridable Overrides`  
  
-   `Shared`  
  
     可选。 请参阅 [共享](../../../visual-basic/language-reference/modifiers/shared.md)。  
  
-   `Shadows`  
  
     可选。 请参阅 [阴影](../../../visual-basic/language-reference/modifiers/shadows.md)。  
  
-   `Async`  
  
     可选。 请参阅 [异步](../../../visual-basic/language-reference/modifiers/async.md)。  
  
-   `Iterator`  
  
     可选。 请参阅 [迭代器](../../../visual-basic/language-reference/modifiers/iterator.md)。  
  
-   `name`  
  
     必需。 该过程的名称。 请参阅 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
-   `typeparamlist`  
  
     可选。 针对泛型过程的类型参数的列表。 请参阅 [键入列表](../../../visual-basic/language-reference/statements/type-list.md)。  
  
-   `parameterlist`  
  
     可选。 表示此过程的参数的本地变量名称的列表。 请参阅 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。  
  
-   `returntype`  
  
     如果使用 `Option Strict` 是 `On`。 此过程所返回的值的数据类型。  
  
-   `Implements`  
  
     可选。 指示此过程实现一个或多个 `Function` 过程，此过程包含类或结构实现的接口中定义每个组。 请参阅 [实现语句](../../../visual-basic/language-reference/statements/implements-statement.md)。  
  
-   `implementslist`  
  
     如果提供 `Implements`，则是必需的。 所实现的 `Function` 过程的列表。  
  
     `implementedprocedure [ , implementedprocedure ... ]`  
  
     每个 `implementedprocedure` 都具有以下语法和部件：  
  
     `interface.definedname`  
  
    |||  
    |-|-|  
    |部件|描述|  
    |`interface`|必需。 此过程所实现的接口名称的包含类或结构。|  
    |`definedname`|必需。 在 `interface` 中用于定义过程的名称。|  
  
-   `Handles`  
  
     可选。 指示此过程可以处理一个或多个特定事件。 请参阅 [处理](../../../visual-basic/language-reference/statements/handles-clause.md)。  
  
-   `eventlist`  
  
     如果提供 `Handles`，则是必需的。 此过程处理的事件的列表。  
  
     `eventspecifier [ , eventspecifier ... ]`  
  
     每个 `eventspecifier` 都具有以下语法和部件：  
  
     `eventvariable.event`  
  
    |||  
    |-|-|  
    |部件|描述|  
    |`eventvariable`|必需。 声明的类或结构，它将引发事件的数据类型的对象变量。|  
    |`event`|必需。 此过程处理的事件的名称。|  
  
-   `statements`  
  
     可选。 此过程中执行的语句块。  
  
-   `End Function`  
  
     终止此过程的定义。  
  
## <a name="remarks"></a>备注  
 在过程内必须是所有可执行代码。 反过来，每个过程，一个类、 结构或包含的类、 结构或模块称为一个模块中声明。  
  
 若要将值返回给调用代码，使用 `Function` 过程; 否则，请使用 `Sub` 过程。  
  
## <a name="defining-a-function"></a>定义函数  
 您可以定义 `Function` 仅在模块级别的过程。 因此，对于函数的声明上下文必须是一个类、 结构、 模块或接口，且不能为源文件、 命名空间、 过程或块。 有关详细信息，请参阅 [声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 `Function` 过程默认为公共访问。 您可以调整它们的访问级别使用的访问修饰符。  
  
 一个 `Function` 过程可以声明该过程返回的值的数据类型。 您可以指定任何数据类型或枚举、 结构、 类或接口的名称。 如果没有指定 `returntype` 参数，则该过程返回 `Object`。  
  
 如果此过程使用 `Implements` 关键字、 包含的类或结构还必须具有 `Implements` 紧跟在后面的语句及其 `Class` 或 `Structure` 语句。  `Implements` 语句必须包含在指定的每个接口 `implementslist`。 但是，通过该接口定义的名称 `Function` (在 `definedname`) 不需要此过程的名称匹配 (在 `name`)。  
  
> [!NOTE]
>  可以使用 lambda 表达式来定义内联函数的表达式。 有关详细信息，请参阅 [函数表达式](../../../visual-basic/language-reference/operators/function-expression.md) 和 [Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
## <a name="returning-from-a-function"></a>从函数返回  
 当 `Function` 过程返回到调用代码时，继续执行调用该过程的语句后面的语句。  
  
 若要从函数返回一个值，可以将该值赋给出函数名称，或将其包含在 `Return` 语句。  
  
  `Return` 语句同时分配返回值，并退出函数，如以下示例所示。  
  
 [!code-vb[VbVbalrStatements#24](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/function-statement_1.vb)]  
  
 下面的示例将返回值分配给函数名 `myFunction` ，然后使用 `Exit Function` 语句返回。  
  
 [!code-vb[VbVbalrStatements#23](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/function-statement_2.vb)]  
  
  `Exit Function` 和 `Return` 语句会导致立即退出 `Function` 过程。 任意数量的 `Exit Function` 和 `Return` 语句可以在过程中，任何位置出现，并可混合 `Exit Function` 和 `Return` 语句。  
  
 如果您使用 `Exit Function` 而不将分配到的值 `name`, ，该过程返回在指定的数据类型的默认值 `returntype`。 如果 `returntype` 未指定，则该过程返回 `Nothing`, ，这是默认值为 `Object`。  
  
## <a name="calling-a-function"></a>调用函数  
 您调用 `Function` 过程的方法是使用过程名，跟在括号内，在表达式中的参数列表。 只有在不提供任何参数，可以省略括号。 但是，您的代码是始终包含括号更具可读性。  
  
 您调用 `Function` 过程相同的方式调用的任何库函数如 `Sqrt`, ，`Cos`, ，或 `ChrW`。  
  
 您还可以通过调用一个函数 `Call` 关键字。 在这种情况下，将忽略返回值。 利用 `Call` 关键字，则不建议在大多数情况下。 有关详细信息，请参阅 [Call 语句](../../../visual-basic/language-reference/statements/call-statement.md)。  
  
 Visual Basic 有时可以重新排列算术表达式来提高内部工作效率。 由于这个原因，不应使用 `Function` 算术表达式时该函数更改同一表达式中的变量的值中的过程。  
  
## <a name="async-functions"></a>异步函数  
  *异步* 功能可用于调用异步函数而无需使用显式回调或手动将您的代码分拆跨多个函数或 lambda 表达式。  
  
 如果将标记与函数 [异步](../../../visual-basic/language-reference/modifiers/async.md) 修饰符，您可以使用 [Await](../../../visual-basic/language-reference/operators/await-operator.md) 函数中的运算符。 当控制达到 `Await` 中的表达式 `Async` 函数，控制权将返回给调用方，并且等待的任务完成之前一直于挂起在函数中的进度。 当任务完成后时，可在函数中恢复执行。  
  
> [!NOTE]
>   `Async` 过程将返回给调用方时也遇到尚未完成，第一个 awaited 的对象或到达末尾 `Async` 过程中，无论哪个操作发生第一次。  
  
  `Async` 函数可以具有返回类型为 <xref:System.Threading.Tasks.Task%601> 或 <xref:System.Threading.Tasks.Task>。 举例说明如何 `Async` 函数的返回类型为 <xref:System.Threading.Tasks.Task%601> 下面提供了。  
  
  `Async` 函数不能声明任何 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) 参数。  
  
 一个 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md) 还可以使用标记 `Async` 修饰符。 这主要用于事件处理程序，不能返回一个值的位置。  `Async``Sub` 过程不能处于等待状态，并且调用方的 `Async``Sub` 过程不能捕获所引发异常的 `Sub` 过程。  
  
 有关详细信息 `Async` 函数，请参见 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md), ，[异步程序中的控制流](../Topic/Control%20Flow%20in%20Async%20Programs%20\(C%23%20and%20Visual%20Basic\).md), ，和 [异步返回类型](../Topic/Async%20Return%20Types%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## <a name="iterator-functions"></a>迭代器函数  
  *迭代器* 函数执行自定义迭代访问集合，如列表或数组。 迭代器函数使用 [产生](../../../visual-basic/language-reference/statements/yield-statement.md) 语句可一次返回每个元素。 当 [产生](../../../visual-basic/language-reference/statements/yield-statement.md) 到达语句，记住代码中的当前位置。 在下次调用迭代器函数将从该位置重新开始执行。  
  
 通过使用从客户端代码调用迭代器 [为每个...下一步](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 语句。  
  
 迭代器函数的返回类型可以是 <xref:System.Collections.IEnumerable>, ，<xref:System.Collections.Generic.IEnumerable%601>, ，<xref:System.Collections.IEnumerator>, ，或 <xref:System.Collections.Generic.IEnumerator%601>。  
  
 有关更多信息，请参见 [迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## <a name="example"></a>示例  
 下面的示例使用 `Function` 语句来声明名称、 参数和窗体的主体的代码 `Function` 过程。  `ParamArray` 修饰符将启用用于接受可变数量的参数的函数。  
  
 [!code-vb[VbVbalrStatements#25](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/function-statement_3.vb)]  
  
## <a name="example"></a>示例  
 下面的示例调用在前面的示例声明的函数。  
  
 [!code-vb[VbVbalrStatements#26](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/function-statement_4.vb)]  
  
## <a name="example"></a>示例  
 在下面的示例中， `DelayAsync` 是 `Async``Function` 具有返回类型的 <xref:System.Threading.Tasks.Task%601>。 `DelayAsync` 具有返回整数的 `Return` 语句。 因此的函数声明 `DelayAsync` 需要具有返回类型的 `Task(Of Integer)`。 因为返回类型为 `Task(Of Integer)`, ，计算 `Await` 中的表达式 `DoSomethingAsync` 产生一个整数。 在此语句中对此进行了演示︰ `Dim result As Integer = Await delayTask`。  
  
  `startButton_Click` 过程是一种 `Async Sub` 过程。 因为 `DoSomethingAsync` 是 `Async` 函数，以调用任务 `DoSomethingAsync` 必须等待，如下面的语句所示︰ `Await DoSomethingAsync()`。  `startButton_Click``Sub` 过程必须定义与 `Async` 修饰符，因此 `Await` 表达式。  
  
 [!code-vb[csAsyncMethod#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/visualbasic/asyncfunctionvb/mainwindow.xaml.vb#1)]  
  
## <a name="see-also"></a>另请参阅  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function 过程](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Call 语句](../../../visual-basic/language-reference/statements/call-statement.md)   
 [的](../../../visual-basic/language-reference/statements/of-clause.md)   
 [参数数组](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [如何︰ 使用泛型类](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [故障排除过程](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [函数表达式](../../../visual-basic/language-reference/operators/function-expression.md)