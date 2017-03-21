---
title: "For Each...Next 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ForEach"
  - "vb.ForEachNext"
  - "vb.Each"
  - "ForEachNext"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "无限循环"
  - "下一个语句，For Each...Next"
  - "无限循环"
  - "循环结构，For Each...Next"
  - "循环, 无限"
  - "Each 关键字"
  - "指令, 重复"
  - "For Each 语句"
  - "集合，指令重复"
  - "循环, 无限"
  - "For Each...Next 语句"
  - "For 关键字 [Visual Basic]，For Each...Next 语句"
  - "Exit 语句，For Each...Next 语句"
  - "迭代"
ms.assetid: ebce3120-95c3-42b1-b70b-fa7da40c75e2
caps.latest.revision: 56
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 56
---
# For Each...Next 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对于集合中的每个元素重复一组语句。  
  
## 语法  
  
```  
For Each element [ As datatype ] In group  
    [ statements ]  
    [ Continue For ]  
    [ statements ]  
    [ Exit For ]  
    [ statements ]  
Next [ element ]  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`element`|在 `For Each` 语句中是必选项。  在 `Next` 语句中是可选项。  变量。  用于循环访问集合的元素。|  
|`datatype`|必需，如果 `element` 尚未声明。  `element` 的数据类型。|  
|`group`|必需。  与集合类型或对象的类型的变量。  引用要重复 `statements` 的集合。|  
|`statements`|可选。  `For Each` 和 `Next` 之间的一条或多条语句，这些语句在 `group` 中的每一项上运行。|  
|`Continue For`|可选。  将控制转移到 `For Each` 循环的开始。|  
|`Exit For`|可选。  将控制转移到 `For Each` 循环外。|  
|`Next`|必需。  终止 `For Each` 循环的定义。|  
  
## 简单示例  
 当需要为集合或数组的每个元素重复执行一组语句时，请使用 `For Each`...`Next` 循环。  
  
> [!TIP]
>  当可以将循环的每次迭代与控制变量相关联并可确定该变量的初始值和最终值时，[For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md) 非常适合。  但是，那么，当您处理集合时，最初和最终值的概念不是有意义的，因此，您不必了解多少个元素集合都有。  在这种情况下，`For Each`…`Next` 循环通常是更好的选择。  
  
 在下面的示例中，`For Each`…`Next` 语句通过列表集合的所有元素。  
  
 [!code-vb[VbVbalrStatements#121](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_1.vb)]  
  
 有关更多示例，请参见[集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)和[数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
## 嵌套的循环  
 可以将一个循环放在另一个循环内以嵌套 `For Each` 循环。  
  
 下面的示例演示嵌套 `For Each`…`Next` 结构。  
  
 [!code-vb[VbVbalrStatements#122](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_2.vb)]  
  
 在嵌套循环时，每个循环必须具有唯一 `element` 变量。  
  
 您还可以将多个不同类型的控制结构相互进行嵌套。  有关更多信息，请参见[嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)。  
  
## 退出并继续为  
 [退出。](../../../visual-basic/language-reference/statements/exit-statement.md) 语句导致执行退出 `For`…循环`Next` 并将控制转移到遵循 `Next` 条语句。  
  
 `Continue For` 语句将控制权立即转移给下一轮循环。  有关更多信息，请参见[Continue 语句](../../../visual-basic/language-reference/statements/continue-statement.md)。  
  
 下面的示例显示如何使用 `Continue For` 和 `Exit For` 语句。  
  
 [!code-vb[VbVbalrStatements#123](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_3.vb)]  
  
 可以在 `For Each` 循环中放置任意数量的 `Exit For` 语句。  当在嵌套的 `For Each` 循环内使用时，`Exit For` 会致使执行退出最内层的循环，并将控制权交给下一层较高级别的嵌套。  
  
 `Exit For` 通常在计算特定条件后使用，例如在 `If`...`Then`...`Else` 结构中。  您可能希望针对下列条件使用 `Exit For`：  
  
-   继续循环不必要或不可能。  这可能是由错误的值或终止请求引起的。  
  
-   在 `Try`...`Catch`...`Finally` 中捕获异常。  可以在 `Finally` 块的末尾使用 `Exit For`。  
  
-   存在无限循环，这种循环可能会运行很多次甚至无限次。  如果检测到这样的条件，就可以使用 `Exit For` 退出循环。  有关更多信息，请参见[Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)。  
  
## 迭代器  
 使用的 *迭代器* 对集合的自定义迭代。  迭代器可以是函数或 `Get` 访问器。  它使用一个 `Yield` 语句返回集合中的每个元素一个节点。  
  
 使用 `For Each...Next` 语句，则调用迭代器。  `For Each` 循环的每次迭代调用迭代器。  当 `Yield` 语句在迭代器时为止，在 `Yield` 语句中的表达式返回，并且，代码的当前位置保留。  执行从该位置下次重新启动迭代器调用。  
  
 下面的示例使用一个迭代器函数。  迭代器函数具有是在 [for…next](../../../visual-basic/language-reference/statements/for-next-statement.md) 循环内的一个 `Yield` 语句。  在 `ListEvenNumbers` 方法，`For Each` 语句体的每个迭代创建对迭代器函数，执行下一 `Yield` 语句。  
  
 [!code-vb[VbVbalrStatements#127](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_4.vb)]  
  
 有关更多信息，请参见[迭代器](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)、[Yield 语句](../../../visual-basic/language-reference/statements/yield-statement.md)和[迭代器](../../../visual-basic/language-reference/modifiers/iterator.md)。  
  
## 技术实现  
 当 `For Each`…`Next` 语句运行时，Visual Basic 计算仅收集一次，因此，在循环开始之前。  如果您的语句块更改 `element` 或 `group`，这些更改不会影响循环的迭代。  
  
 在连续地将集合中的所有元素分配给 `element` 后，`For Each` 循环停止，并将控制权传递给 `Next` 语句后面的语句。  
  
 如果 `element` 未在循环外声明，则必须将其声明为在 `For Each` 语句。  可以使用 `As` 语句显式声明 `element` 的类型，也可以依赖类型推断来分配该类型。  在任意一种情况下，`element` 的范围都是循环的主体。  但是，不能既在循环外又在循环内声明 `element`。  
  
 可以选择在 `Next` 语句中指定 `element`。  这将提高程序的可读性，尤其是在具有嵌套的 `For Each` 循环的情况下。  必须指定与相应的 `For Each` 语句中出现的变量相同的变量。  
  
 您可能希望避免在循环中更改 `element` 的值。  这样做可能会更难以阅读和调试代码。  更改 `group` 的值不会影响集合或其组件，确定的，当循环先输入了。  
  
 在嵌套循环，因此，如果一个外部嵌套级别的 `Next` 语句在内部级别的 `Next` 之前遇到，编译器发出错误信号。  不过，仅当在所有 `Next` 语句中都指定了 `element` 时，编译器才能检测到这种重叠错误。  
  
 如果您的代码依赖于遍历集合按特定顺序，`For Each`…`Next` 循环不是最佳选择，除非您知道集合公开 enumerator 对象的属性。  遍历顺序未由 Visual Basic 中，但是 enumerator 对象的 <xref:System.Collections.IEnumerator.MoveNext%2A> 方法。  因此，您可能无法预测 `element` 中首先返回集合中的哪个元素，或者在某个给定的元素后返回的下一个元素是哪个元素。  使用其他循环结构（如 `For`...`Next` 或 `Do`...`Loop`）可能会获得更可靠的结果.  
  
 `element` 的数据类型必须是 `group` 的元素的数据类型可以转换成的类型。  
  
 `group` 的数据类型必须是引用集合或数组是可枚举的引用类型。  通常情况下，这意味着 `group` 将引用实现 <xref:System.Collections.IEnumerable> 命名空间 `System.Collections` 的接口或 <xref:System.Collections.Generic.IEnumerable%601> 命名空间 `System.Collections.Generic` 的接口。  `System.Collections.IEnumerable` 定义 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 方法，而该方法返回集合的枚举数对象。  枚举数对象实现 `System.Collections` 命名空间的 `System.Collections.IEnumerator` 接口，并公开 <xref:System.Collections.IEnumerator.Current%2A> 属性以及 <xref:System.Collections.IEnumerator.Reset%2A> 和 <xref:System.Collections.IEnumerator.MoveNext%2A> 方法。  Visual Basic 使用它们遍历集合。  
  
### 收缩转换  
 当 `Option Strict` 设置为 `On` 时，收缩转换通常会导致编译器错误。  但是，在 `For Each` 中，会在运行时计算并执行从 `group` 中的元素到 `element` 的转换，并禁止显示收缩转换引起的编译器错误。  
  
 在下面的示例中，`m` 的指定作为 `n` 的初始值不生成 `Option Strict` 打开时，因为 `Long` 转换为 `Integer` 与收缩转换。  但是，在 `For Each` 语句中，没有报告编译器错误，即使对 `number` 的赋值同样需要由 `Long` 转换为  `Integer`。  在包含一个大数字的 `For Each` 语句中，在将 <xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A> 应用于该大数字时，出现运行时错误。  
  
 [!code-vb[VbVbalrStatements#89](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_5.vb)]  
  
### IEnumerator 调用  
 开始执行 `For Each`...`Next` 循环时，Visual Basic 将检查 `group` 是否引用有效的集合对象。  如果不是，它将引发异常。  否则，它调用枚举数对象的 <xref:System.Collections.IEnumerator.MoveNext%2A> 方法和 <xref:System.Collections.IEnumerator.Current%2A> 属性以返回第一个元素。  如果 `MoveNext` 指示没有下一个元素，即集合为空，则 `For Each` 循环停止，并将控制权传递到 `Next` 语句后面的语句。  否则，Visual Basic 将 `element` 设置为第一个元素，并运行语句块。  
  
 Visual Basic 每次遇到 `Next` 语句时，都返回至 `For Each` 语句。  它将再次调用 `MoveNext` 和 `Current` 以返回下一个元素，然后根据结果再次运行块或者停止循环。  此过程将继续，直至 `MoveNext` 指示没有下一个元素或者遇到 `Exit For` 语句为止。  
  
 **修改集合。** <xref:System.Collections.IEnumerable.GetEnumerator%2A> 返回的枚举数对象通常不允许您通过添加，删除，替换或重新排列任何元素更改集合。  如果在启动 `For Each`...`Next` 循环后更改了集合，枚举数对象将失效，并且下次尝试访问元素时将引发 <xref:System.InvalidOperationException> 异常。  
  
 但是，此块修改未由 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]，而是 <xref:System.Collections.IEnumerable> 接口的实现。  在实现 `IEnumerable` 时可以允许在迭代期间进行修改。  如果要进行这种动态修改，请确保您对所用集合 `IEnumerable` 实现的特点有很好的理解。  
  
 **修改集合元素。**枚举数对象的 <xref:System.Collections.IEnumerator.Current%2A> 属性为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)，它返回每个集合元素的本地副本。  这意味着不能在 `For Each`...`Next` 循环中修改元素本身。  所有修改由 `Current` 进行只影响该本地副本并不反映回基础集合。  但是，如果元素属于引用类型，则可以修改它所指向的实例的成员。  下面的示例修改每个 `thisControl` 元素的 `BackColor` 成员。  无法，但是，修改 `thisControl`。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 前面的示例可以修改每个 `thisControl` 元素的 `BackColor` 成员，但是不能修改 `thisControl` 自身。  
  
 **遍历数组。**由于 <xref:System.Array> 类实现了 <xref:System.Collections.IEnumerable> 接口，因此所有数组都公开 <xref:System.Array.GetEnumerator%2A> 方法。  这意味着可以使用 `For Each`...`Next` 循环来循环访问数组。  但是，只能读取数组元素。  这些项无法更改。  
  
## 示例  
 下面的示例使用 <xref:System.IO.DirectoryInfo> 类列出 C:\\ 目录下的所有文件夹。  
  
 [!code-vb[VbVbalrStatements#124](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_6.vb)]  
  
## 示例  
 下面的示例演示排序的集合的方法。  该示例对 <xref:System.Collections.Generic.List%601>存储 `Car` 选件类的实例。  `Car` 选件类实现 <xref:System.IComparable%601> 接口，需要 <xref:System.IComparable%601.CompareTo%2A> 方法执行。  
  
 每个调用 <xref:System.IComparable%601.CompareTo%2A> 方法使用于排序的唯一比较。  在 `CompareTo` 方法的用户编写的代码将当前对象的每个比较的值与其他对象的。  返回的值小于零，如果当前对象与另一个对象小于，大于零，如果当前对象大于另一个对象和零，则它们相等。  这使您可以定义代码大的标准相比，比和相等。  
  
 在 `ListCars` 方法，`cars.Sort()` 语句对列表进行排序。  这对 <xref:System.Collections.Generic.List%601> 原因的 <xref:System.Collections.Generic.List%601.Sort%2A> 方法为 `List`的 `Car` 对象将自动调用的 `CompareTo` 方法。  
  
 [!code-vb[VbVbalrStatements#125](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_7.vb)]  
  
## 请参阅  
 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [循环结构](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [While...End While 语句](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [对象初始值设定项：命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)