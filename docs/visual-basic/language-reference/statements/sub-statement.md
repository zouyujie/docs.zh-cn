---
title: "Sub 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Sub"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Public 关键字，Sub 语句"
  - "创建的过程"
  - "声明过程，Sub 语句"
  - "变量 [Visual Basic] Sub 过程"
  - "As 关键字，Sub 语句"
  - "可选关键字，Sub 语句"
  - "声明过程"
  - "Sub 关键字"
  - "Handles 关键字，Sub 语句"
  - "Protected Friend 关键字"
  - "ParamArray 关键字，Sub 语句"
  - "Implements 关键字，Sub 语句"
  - "Sub 语句"
  - "子例程"
  - "ByRef 关键字，Sub 语句"
  - "Sub 语句的 sub 过程"
  - "递归过程"
  - "Private 关键字，Sub 语句"
  - "Friend 关键字，Sub 语句"
  - "Exit 语句，Sub 语句"
  - "Sub 过程"
  - "End 关键字，Sub 语句"
  - "ByVal 关键字，Sub 语句"
  - "Visual Basic 代码，Sub 过程"
ms.assetid: e347d700-d06c-405b-b302-e9b1edb57dfc
caps.latest.revision: 52
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 52
---
# Sub 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明名称、 参数和定义的代码 `Sub` 过程。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attributelist> ] [ Partial ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async ]  
Sub name [ (Of typeparamlist) ] [ (parameterlist) ] [ Implements implementslist | Handles eventlist ]  
    [ statements ]  
    [ Exit Sub ]  
    [ statements ]  
End Sub  
```  
  
## <a name="parts"></a>部件  
  
-   `attributelist`  
  
     可选。 请参阅 [属性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
-   `Partial`  
  
     可选。 指示分部方法的定义。 请参阅 [分部方法](../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)。  
  
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
  
-   `name`  
  
     必需。 该过程的名称。 请参阅 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。 若要创建一个类的构造函数过程，请将名称设置 `Sub` 过程 `New` 关键字。 有关详细信息，请参阅 [对象生存期︰ 对象的方式创建和破坏](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)。  
  
-   `typeparamlist`  
  
     可选。 针对泛型过程的类型参数的列表。 请参阅 [键入列表](../../../visual-basic/language-reference/statements/type-list.md)。  
  
-   `parameterlist`  
  
     可选。 表示此过程的参数的本地变量名称的列表。 请参阅 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。  
  
-   `Implements`  
  
     可选。 指示此过程实现一个或多个 `Sub` 过程，此过程包含类或结构实现的接口中定义每个组。 请参阅 [实现语句](../../../visual-basic/language-reference/statements/implements-statement.md)。  
  
-   `implementslist`  
  
     如果提供 `Implements`，则是必需的。 所实现的 `Sub` 过程的列表。  
  
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
  
     可选。 要在此过程中运行的语句块。  
  
-   `End Sub`  
  
     终止此过程的定义。  
  
## <a name="remarks"></a>备注  
 在过程内必须是所有可执行代码。 使用 `Sub` 过程时不想将值返回给调用代码。 使用 `Function` 过程时想要返回一个值。  
  
## <a name="defining-a-sub-procedure"></a>定义一个 Sub 过程  
 您可以定义 `Sub` 仅在模块级别的过程。 Sub 过程的声明上下文，因此，必须类、 结构、 模块或接口，且不能为源文件、 命名空间、 过程或块。 有关详细信息，请参阅 [声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 `Sub` 过程默认为公共访问。 通过使用访问修饰符，可以调整它们的访问级别。  
  
 如果该过程使用 `Implements` 关键字、 包含的类或结构必须具有 `Implements` 紧跟在后面的语句及其 `Class` 或 `Structure` 语句。  `Implements` 语句必须包含在指定的每个接口 `implementslist`。 但是，通过该接口定义的名称 `Sub` (在 `definedname`) 无需与此过程的名称相匹配 (在 `name`)。  
  
## <a name="returning-from-a-sub-procedure"></a>返回从一个 Sub 过程  
 当 `Sub` 过程返回到调用代码时，继续执行后调用它的语句的语句。  
  
 下面的示例演示从返回 `Sub` 过程。  
  
```vb#  
Sub mySub(ByVal q As String)  
    Return  
End Sub   
```  
  
  `Exit Sub` 和 `Return` 语句会导致立即退出 `Sub` 过程。 任意数量的 `Exit Sub` 和 `Return` 语句可以在过程中，任何位置出现，并可混合 `Exit Sub` 和 `Return` 语句。  
  
## <a name="calling-a-sub-procedure"></a>调用一个 Sub 过程  
 您调用 `Sub` 过程的方法是在一个语句中使用的过程名，然后按照该名称与在括号中的参数列表。 仅当您不提供任何参数，可以省略括号。 但是，您的代码是始终包含括号更具可读性。  
  
 一个 `Sub` 过程和一个 `Function` 过程可以具有参数，并执行一系列语句。 但是， `Function` 过程返回一个值，并 `Sub` 过程不会。 因此，不能使用 `Sub` 在表达式中的过程。  
  
 您可以使用 `Call` 关键字调用时 `Sub` 过程中，但该关键字，则不建议大多数应用中。 有关详细信息，请参阅 [Call 语句](../../../visual-basic/language-reference/statements/call-statement.md)。  
  
 Visual Basic 有时可以重新排列算术表达式来提高内部工作效率。 因此，如果参数列表包含表达式调用其他过程，您不应假定，将按特定顺序调用这些表达式。  
  
## <a name="async-sub-procedures"></a>Async Sub 过程  
 通过使用异步功能，可以调用异步函数，而无需使用显式回调或手动将您的代码分拆跨多个函数或 lambda 表达式。  
  
 如果您将过程标记为与 [异步](../../../visual-basic/language-reference/modifiers/async.md) 修饰符，您可以使用 [Await](../../../visual-basic/language-reference/operators/await-operator.md) 过程中的运算符。 当控制达到 `Await` 中的表达式 `Async` 过程中，控件返回到调用方，并等待的任务完成之前一直于挂起过程中的进度。 当任务完成后时，执行可恢复过程中。  
  
> [!NOTE]
>   `Async` 过程将返回到调用方遇到任一的第一个处于等待状态的对象尚未完成时或结束的 `Async` 达到过程时，无论哪个操作先发生。  
  
 你还可以标记 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md) 与 `Async` 修饰符。  `Async` 函数可以具有返回类型为 <xref:System.Threading.Tasks.Task%601> 或 <xref:System.Threading.Tasks.Task>。 示例更高版本在本主题演示 `Async` 函数的返回类型为 <xref:System.Threading.Tasks.Task%601>。  
  
 `Async` `Sub` 过程主要用于事件处理程序，不能返回一个值的位置。  `Async``Sub` 过程不能处于等待状态，并且调用方的 `Async``Sub` 过程不能捕获异常， `Sub` 过程，则会引发。  
  
  `Async` 过程不能声明任何 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) 参数。  
  
 有关详细信息 `Async` 过程，请参阅 [使用 Async 和 Await 的异步编程](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md), ，[异步程序中的控制流](../Topic/Control%20Flow%20in%20Async%20Programs%20\(C%23%20and%20Visual%20Basic\).md), ，和 [异步返回类型](../Topic/Async%20Return%20Types%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## <a name="example"></a>示例  
 下面的示例使用 `Sub` 语句来定义名称、 参数和窗体的主体的代码 `Sub` 过程。  
  
 [!code-vb[VbVbalrStatements#58](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/sub-statement_1.vb)]  
  
## <a name="example"></a>示例  
 在下面的示例中， `DelayAsync` 是 `Async``Function` 具有返回类型的 <xref:System.Threading.Tasks.Task%601>。 `DelayAsync` 具有返回整数的 `Return` 语句。 因此，函数声明的 `DelayAsync` 必须具有返回类型的 `Task(Of Integer)`。 因为返回类型为 `Task(Of Integer)`, ，计算 `Await` 中的表达式 `DoSomethingAsync` 产生一个整数，如以下语句所示︰ `Dim result As Integer = Await delayTask`。  
  
  `startButton_Click` 过程是一种 `Async Sub` 过程。 因为 `DoSomethingAsync` 是 `Async` 函数，以调用任务 `DoSomethingAsync` 必须等待，如以下语句所示︰ `Await DoSomethingAsync()`。  `startButton_Click``Sub` 过程必须定义与 `Async` 修饰符，因此 `Await` 表达式。  
  
 [!code-vb[csAsyncMethod#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/VisualBasic/sub-statement_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Call 语句](../../../visual-basic/language-reference/statements/call-statement.md)   
 [的](../../../visual-basic/language-reference/statements/of-clause.md)   
 [参数数组](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [如何︰ 使用泛型类](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [故障排除过程](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [分部方法](../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)