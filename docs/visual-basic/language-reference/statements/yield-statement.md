---
title: "Yield 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Yield"
helpviewer_keywords: 
  - "迭代器, Yield 语句 [Visual Basic]"
  - "迭代器 [Visual Basic]"
  - "Yield 语句 [Visual Basic]"
ms.assetid: f33126c5-d7c4-43e2-8e36-4ae3f0703d97
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Yield 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

发送集合中的下一个元素。`For Each...Next` 语句。  
  
## 语法  
  
```  
Yield expression  
```  
  
#### 参数  
  
|||  
|-|-|  
|术语|定义|  
|`expression`|必需。  隐式转换为迭代器函数或 `Get` 访问器的类型包含 `Yield` 语句的表达式。|  
  
## 备注  
 `Yield` 语句次返回集合中的元素。  `Yield` 语句在迭代器函数或 `Get` 访问器，包括对集合的自定义迭代。  
  
 使用 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 或 LINQ 查询，则使用迭代器函数。  `For Each` 循环的每次迭代调用迭代器函数。  当 `Yield` 语句在迭代器函数时为止，`expression` 返回，并且，代码的当前位置保留。  执行从该位置下次重新启动迭代器函数调用。  
  
 隐式转换必须从 `expression` 的类型。`Yield` 语句的提供给迭代器的返回类型。  
  
 可以使用 `Exit Function` "或 `Return` 语句结束迭代。  
  
 只有 \+ 当用于 `Iterator` 函数或 `Get` 访问器时，“生成”不是保留字并具有特殊含义。  
  
 有关迭代器函数和 `Get` 访问器的更多信息，请参见 [迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 迭代器函数和 get 访问器  
 迭代器函数或 `Get` 访问器的声明必须满足以下要求：  
  
-   它必须包含 [迭代器](../../../visual-basic/language-reference/modifiers/iterator.md) 修饰符。  
  
-   返回类型必须是 <xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601>、<xref:System.Collections.IEnumerator>或 <xref:System.Collections.Generic.IEnumerator%601>。  
  
-   它不能有任何 `ByRef` 参数。  
  
 迭代器函数在事件、实例构造函数、静态构造函数或静态析构函数不能出现。  
  
 迭代器函数可以是匿名函数。  有关更多信息，请参见[迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 异常处理  
 `Yield` 语句将在 `Try` 块 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  `Try` 块有一个 `Yield` 语句可以具有 `Catch` 块，并可以具有 `Finally` 块。  
  
 `Yield` 语句不能在 `Catch` 块或 `Finally` 块。  
  
 如果 `For Each` 主体 \(在迭代器函数之外\) 引发异常，`Catch` 在迭代器功能块，不会执行，但 `Finally` 在迭代器功能块中执行。  `Catch` 块在迭代器功能出现在迭代器函数内仅捕获的异常中。  
  
## 技术实现  
 下面的代码从返回的迭代器函数的 `IEnumerable (Of String)` 通过 `IEnumerable (Of String)`的元素然后重复。  
  
```vb  
Dim elements As IEnumerable(Of String) = MyIteratorFunction()  
    …  
For Each element As String In elements  
Next  
```  
  
 为 `MyIteratorFunction` 的调用不执行该函数体。  而是调用返回 `IEnumerable(Of String)` 到 `elements` 变量中。  
  
 在 `For Each` 循环迭代中，<xref:System.Collections.IEnumerator.MoveNext%2A> 方法。`elements`调用。  这称为执行 `MyIteratorFunction` 主体，直至下一个 `Yield` 语句为止。  `Yield` 语句返回由循环体确定 `element` 变量的值不仅消耗的，而且元素 <xref:System.Collections.Generic.IEnumerator%601.Current%2A> 属性，是 `IEnumerable (Of String)`的表达式。  
  
 在 `For Each` 循环的每个后续迭代中，迭代器体中执行从延续它将会停止的位置，再次停止，在到达 `Yield` 语句时。  在迭代器函数或 `Return` 或 `Exit Function` 语句的结尾时，`For Each` 循环完成。  
  
## 示例  
 下面的示例有在 [for…next](../../../visual-basic/language-reference/statements/for-next-statement.md) 循环内的一个 `Yield` 语句。  [对于每个](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 语句体的每个迭代在 `Main` 的创建调用 `Power` 迭代器函数。  每个调用迭代器函数提升到 `Yield` 语句的下执行，在 `For…Next` 循环的下一次迭代时发生。  
  
 迭代器方法的返回类型为 <xref:System.Collections.Generic.IEnumerable%601>，迭代器接口类型。  在迭代器方法被调用时，它返回一个的幂的可枚举对象。  
  
 [!code-vb[VbVbalrStatements#98](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/yield-statement_1.vb)]  
  
## 示例  
 下面的示例演示是迭代器的 `Get` 访问器。  属性声明包含一个 `Iterator` 修饰符。  
  
 [!code-vb[VbVbalrStatements#99](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/yield-statement_2.vb)]  
  
 有关其他示例，请参见[迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 要求  
 [!INCLUDE[vs_dev11_long](../../../csharp/includes/vs-dev11-long-md.md)]  
  
## 请参阅  
 [迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)   
 [语句](../../../visual-basic/language-reference/statements/index.md)