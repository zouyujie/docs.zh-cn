---
title: "可以为 Null 的值类型 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Nullable"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "? [Visual Basic]"
  - "数据类型 [Visual Basic], 可以为 null"
  - "可以为 null 的类型"
  - "可以为 null 的类型 [Visual Basic]"
  - "类型 [Visual Basic], 可以为 null"
ms.assetid: 9ac3b602-6f96-4e6d-96f7-cd4e81c468a6
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# 可以为 Null 的值类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

有时候，您会使用在某些情况下没有已定义值的值类型。  例如，数据库中的字段可能需要区分已赋予一个有意义的值与尚未赋值这两种情况。  可以扩展值类型，使它们具有正常值或 null 值。  此类扩展称为可以为 null 的类型。  
  
 每一种可以为 null 的类型均从 <xref:System.Nullable%601> 泛型结构中构造。  请考虑一个跟踪工作相关活动的数据库。  下面的示例构造一个可以为 null 的 `Boolean` 类型，并声明该类型的一个变量。  可以通过以下三种方式来编写声明：  
  
 [!code-vb[VbVbalrNullableValue#1](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_1.vb)]  
  
 变量 `ridesBusToWork` 可以保存值 `True`、值 `False` 或根本不保存值。  其初始默认值是根本没有值，在这种情况下可能表示尚未获得此人的信息。  相反，`False` 可能表示已获得此人的信息，但此人未乘坐公共汽车去上班。  
  
 可以使用可以为 null 的类型来声明变量和属性，也可以使用可以为 null 的类型的元素来声明数组。  可以使用可以为 null 的类型作为参数来声明过程，也可以从 `Function` 过程中返回可以为 null 的类型。  
  
 无法在引用类型（如数组、`String` 或类）上构造可以为 null 的类型。  基础类型必须为值类型。  有关更多信息，请参见 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)。  
  
## 使用可以为 null 的类型的变量  
 可以为 null 的类型的最重要成员是它的 <xref:System.Nullable%601.HasValue%2A> 和 <xref:System.Nullable%601.Value%2A> 属性。  对于可以为 null 的类型的变量，<xref:System.Nullable%601.HasValue%2A> 将指出此变量是否包含已定义的值。  如果 <xref:System.Nullable%601.HasValue%2A> 为 `True`，则可以从 <xref:System.Nullable%601.Value%2A> 中读取值。  请注意，<xref:System.Nullable%601.HasValue%2A> 和 <xref:System.Nullable%601.Value%2A> 均为 `ReadOnly` 属性。  
  
### 默认值  
 如果利用可以为 null 的类型来声明变量，则变量的 <xref:System.Nullable%601.HasValue%2A> 属性具有默认值 `False`。  这意味着，默认情况下，变量没有已定义的值，而不是具有其基础值类型的默认值。  在下面的示例中，变量 `numberOfChildren` 最初没有已定义的值，即使 `Integer` 类型的默认值为 0 也是如此。  
  
 [!code-vb[VbVbalrNullableValue#2](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_2.vb)]  
  
 null 值对于指示未定义的或未知的值很有用。  如果 `numberOfChildren` 已被声明为 `Integer`，则不会有值可以指出当前没有可用的信息。  
  
### 存储值  
 按常规方式将值存储在具有可以为 null 的类型的变量或属性中。  下面的示例将一个值赋予前面示例中所声明的 `numberOfChildren` 变量。  
  
 [!code-vb[VbVbalrNullableValue#3](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_3.vb)]  
  
 如果可以为 null 的类型的变量或属性包含已定义的值，则可以使此变量或属性恢复到其初始状态（即未获分配值）。  可通过将此变量或属性设置为 `Nothing` 来这样做，如下面的示例所示。  
  
 [!code-vb[VbVbalrNullableValue#4](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_4.vb)]  
  
> [!NOTE]
>  尽管可以将 `Nothing` 赋予具有可以为 null 的类型的变量，也不能用等号测试该变量是否为 `Nothing`。  使用等号的比较 \(`someVar = Nothing`\) 的计算结果总是为 `Nothing`。  可以测试该变量的 <xref:System.Nullable%601.HasValue%2A> 属性是否为 `False`，也可以使用 `Is` 或 `IsNot` 运算符进行测试。  
  
### 检索值  
 要检索可以为 null 的类型的变量的值，应先测试它的 <xref:System.Nullable%601.HasValue%2A> 属性，以确认它是否具有值。  如果尝试在 <xref:System.Nullable%601.HasValue%2A> 为 `False` 时读取值，则 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会引发 <xref:System.InvalidOperationException> 异常。  下面的示例演示建议用来读取前面示例的 `numberOfChildren` 变量的方法。  
  
 [!code-vb[VbVbalrNullableValue#5](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_5.vb)]  
  
## 比较可以为 Null 的类型  
 在布尔表达式中使用可以为 null 的 `Boolean` 变量时，结果可能为 `True`、`False` 或 `Nothing`。  下面是 `And` 和 `Or` 的真值表。  因为 `b1` 和 `b2` 现在具有三个可能值，所以要计算九种组合。  
  
|b1|b2|b1 And b2|b1 Or b2|  
|--------|--------|---------------|--------------|  
|`Nothing`|`Nothing`|`Nothing`|`Nothing`|  
|`Nothing`|`True`|`Nothing`|`True`|  
|`Nothing`|`False`|`False`|`Nothing`|  
|`True`|`Nothing`|`Nothing`|`True`|  
|`True`|`True`|`True`|`True`|  
|`True`|`False`|`False`|`True`|  
|`False`|`Nothing`|`False`|`Nothing`|  
|`False`|`True`|`False`|`True`|  
|`False`|`False`|`False`|`False`|  
  
 当布尔变量或表达式的值为 `Nothing` 时，该值既不是 `true`，也不是 `false`。  请看下面的示例。  
  
 [!code-vb[VbVbalrNullableValue#6](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_6.vb)]  
  
 在本示例中，`b1 And b2` 的计算结果为 `Nothing`。  因此，每个 `If` 语句中都会执行 `Else` 子句，其输出如下所示：  
  
 `Expression is not true`  
  
 `Expression is not false`  
  
> [!NOTE]
>  `AndAlso` 和 `OrElse` 使用的是短路计算，当第一个操作数计算结果为 `Nothing` 时，它们必须计算第二个操作数。  
  
## 传播  
 如果算术运算、比较运算、移位运算或类型运算的一个或两个操作数是可以为 null 的值，则运算结果也是可以为 null 的值。  如果两个操作数的值都不是 `Nothing`，则对两个操作数的基础值执行运算，就像它们都不是可以为 null 的类型一样。  在下面的示例中，`compare1` 和 `sum1` 变量进行了隐式类型化。  如果将鼠标指针放置在这两个变量上，则会看到编译器推断它们是可以为 null 的类型。  
  
 [!code-vb[VbVbalrNullableValue#7](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_7.vb)]  
  
 如果其中一个或两个操作数的值为 `Nothing`，则结果将为 `Nothing`。  
  
 [!code-vb[VbVbalrNullableValue#8](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_8.vb)]  
  
## 将可以为 null 的类型用于数据  
 数据库是使用可以为 null 的类型的最重要的地方之一。  当前，并非所有数据库对象都支持可以为 null 的类型，但由设计器生成的表适配器支持这种类型。  请参见 [TableAdapter 概述](/visual-studio/data-tools/tableadapter-overview)中的“TableAdapter 对可以为 null 的类型的支持”。  
  
## 请参阅  
 <xref:System.InvalidOperationException>   
 <xref:System.Nullable%601.HasValue%2A>   
 [使用可以为 null 的类型](../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [TableAdapter 概述](/visual-studio/data-tools/tableadapter-overview)   
 [If 运算符](../../../../visual-basic/language-reference/operators/if-operator.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md)