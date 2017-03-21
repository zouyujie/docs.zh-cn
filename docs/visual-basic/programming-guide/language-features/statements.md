---
title: "语句 (Visual Basic) | Microsoft Docs"
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
  - "蓝色下划线"
  - "冒号 (:)"
  - "常量, 定义"
  - "常量, 语句"
  - "可执行语句"
  - "分行符, 在代码中"
  - "过程, 语句"
  - "语句 [Visual Basic], 关于语句"
  - "下划线"
  - "变量 [Visual Basic], 分配"
  - "变量 [Visual Basic], 声明"
  - "变量 [Visual Basic], 定义"
ms.assetid: fcfdee1a-82b7-4846-98f7-9ca3f5160089
caps.latest.revision: 30
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 30
---
# 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中的语句是完整的指令。  它可以包含关键字、运算符、变量、常数和表达式。  每条语句属于下面两种类别之一：  
  
-   **声明语句**，这种语句命名变量、常数或过程，还可指定数据类型。  
  
-   **可执行语句**，这种语句启动操作。  这些语句可以调用方法或函数，并可以在代码块中循环或分支。  可执行语句包括 **赋值语句**，这种语句将值或表达式赋予变量或常数。  
  
 本主题描述每个类别。  此外，本主题还描述如何在单行上组合多条语句以及如何跨多行继续一条语句。  
  
## 声明语句  
 使用声明语句命名和定义过程、变量、属性、数组和常数。  在声明编程元素时，还可以定义其数据类型、访问级别和范围。  有关更多信息，请参见 [已声明元素的特性](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)。  
  
 下面的示例包含三个声明。  
  
 [!code-vb[VbVbalrStatements#80](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_1.vb)]  
  
 第一个声明是 `Sub` 语句。  与其匹配的 `End Sub` 语句一起，它声明了一个名为 `applyFormat` 的过程。  它还指定 `applyFormat` 是 `Public`，这意味着任何可以引用它的代码都可以调用它。  
  
 第二个声明是 `Const` 语句，该语句声明常数 `limit`，并且指定 `Integer` 数据类型和值 33。  
  
 第三个声明是 `Dim` 语句，它声明变量 `thisWidget`。  数据类型是某个特定对象，即从 `Widget` 类中创建的对象。  可以将变量声明为任何基本数据类型，或声明为在您使用的应用程序中公开的任何对象类型。  
  
### 初始值  
 在包含声明语句的代码运行时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会保留声明的元素所需的内存。  如果该元素具有值，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会将它初始化为其数据类型的默认值。  有关更多信息，请参见 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md) 中的“行为”。  
  
 可以在声明变量的过程中向变量赋予初始值，如下面的示例所示。  
  
 [!code-vb[VbVbalrStatements#81](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_2.vb)]  
  
 如果变量是对象变量，则声明它时可以使用 [New 运算符](../../../visual-basic/language-reference/operators/new-operator.md) 关键字显式创建其类的实例，如下面的示例所示。  
  
 [!code-vb[VbVbalrStatements#82](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_3.vb)]  
  
 请注意，在开始执行变量的声明语句前，您在声明语句中指定的初始值并不会赋给该变量。  在此之前，变量包含的是其数据类型的默认值。  
  
## 可执行语句  
 可执行语句执行一项操作。  它调用过程、分支到代码中的另一个位置、循环执行多个语句中，或计算表达式的值。  赋值语句是可执行语句的一种特殊情况。  
  
 下面的示例使用 `If...Then...Else` 控制结构根据变量的值运行不同的代码块。  在每个代码块内，`For...Next` 循环将运行指定的次数。  
  
 [!code-vb[VbVbalrStatements#83](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_4.vb)]  
  
 前面示例中的 `If` 语句检查参数 `clockwise` 的值。  如果该值为 `True`，它将调用 `aWidget` 的 `spinClockwise` 方法。  如果该值为 `False`，它将调用 `aWidget` 的 `spinCounterClockwise` 方法。  `If...Then...Else` 控制结构以 `End If` 结尾。  
  
 每个块内的 `For...Next` 循环将调用相应的方法一定的次数（与 `revolutions` 参数的值相等）。  
  
## 赋值语句  
 赋值语句执行赋值操作，而赋值操作包括获取赋值运算符 \(`=`\) 右侧的值，并将该值存储到赋值运算符左侧的元素中，如下面的示例所示。  
  
 [!code-vb[VbVbalrStatements#73](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_5.vb)]  
  
 在前面的示例中，赋值语句将文本值 42 存储到变量 `v` 中。  
  
### 合格的编程元素  
 赋值运算符左侧的编程元素必须能够接受和存储值。  这意味着编程元素必须是一个不为 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md) 的变量或属性，或者必须是一个数组元素。  在赋值语句的上下文中，此类元素有时称为 lvalue，即“left value”（左侧的值）。  
  
 赋值运算符右侧的值由表达式生成，而表达式则由文本、常数、变量、属性、数组元素、其他表达式或函数调用的任意组合所构成。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrStatements#74](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_6.vb)]  
  
 前面的示例将变量 `y` 中存储的值与变量 `z` 中存储的值相加，然后与调用函数 `findResult` 返回的值相加。  然后，此表达式的总值将存储到变量 `x` 中。  
  
### 赋值语句中的数据类型  
 除数值外，赋值运算符还可以分配 `String` 值，如下面的示例所阐释。  
  
 [!code-vb[VbVbalrStatements#75](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_7.vb)]  
  
 您也可以使用 `Boolean` 文本或 `Boolean` 表达式分配 `Boolean` 值，如下面的示例所阐释。  
  
 [!code-vb[VbVbalrStatements#76](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_8.vb)]  
  
 同样，您可以将适当的值分配给 `Char`、`Date` 或 `Object` 数据类型的编程元素。  您也可以将对象实例分配给声明作为创建该实例的类的元素。  
  
### 复合赋值语句  
 复合赋值语句先对表达式执行运算，然后才将表达式赋给编程元素。  下面的示例阐释这些运算符中的 `+=`，该运算符使用右侧表达式的值递增运算符左侧变量的值。  
  
 [!code-vb[VbVbalrStatements#77](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_9.vb)]  
  
 前面的示例将 1 与 `n` 的值相加，然后将新值存储在 `n` 中。  它是下列语句的一种简写等效语句：  
  
 [!code-vb[VbVbalrStatements#78](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_10.vb)]  
  
 可以使用此类型的运算符执行各种复合赋值运算。  有关这些运算符的列表及其更多信息，请参见 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)。  
  
 当向已经存在的字符串的末尾添加字符串时，串联赋值运算符 \(`&=`\) 很有用，如下面的示例所阐释。  
  
 [!code-vb[VbVbalrStatements#79](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_11.vb)]  
  
### 赋值语句中的类型转换  
 分配给变量、属性或数组元素的值必须是适合于该目标元素的数据类型。  通常，应当尝试生成与目标元素的数据类型相同的值。  但是，在赋值过程中，一些类型可以转换为其他类型。  
  
 有关在数据类型之间转换的信息，请参见 [Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)。  简言之，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 自动将给定类型的值转换成其扩大至的任何其他类型。  “扩大转换”是在运行时始终成功的转换方式，而且不会丢失任何数据。  例如，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 在适当的时候将 `Integer` 值转换为 `Double` 值，因为 `Integer` 可扩大为 `Double`。  有关更多信息，请参见[扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
 “收缩转换”（那些没有扩展的转换）具有在运行时失败或丢失数据的风险。  您可以通过使用类型转换函数显式执行收缩转换，也可以通过设置 `Option Strict Off` 指示编译器隐式执行所有的转换。  有关更多信息，请参见[隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)。  
  
## 一行中放入多条语句  
 在一行中可以有多条语句，语句之间用冒号 \(`:`\) 字符分隔。  下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrStatements#70](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_12.vb)]  
  
 虽然这种形式的语法偶尔带来方便，但是它使代码难以阅读和维护。  因此，建议您保持一行一条语句。  
  
## 跨多行继续一条语句  
 通常一行容纳一条语句，但当语句太长时，可以使用行继续符在下一行继续该语句，而行继续符依次包含一个空格、一个下划线字符 \(`_`\) 和一个回车符。  在下面的示例中，`MsgBox` 可执行语句连续跨两行。  
  
 [!code-vb[VbVbalrStatements#71](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_13.vb)]  
  
### 隐式行继续  
 在许多情况下，可以在下一连续行上继续一条语句，而无须使用下划线字符 \(\_\)。  下表列出了在下一代码行隐式继续该语句的语法元素。  
  
|||  
|-|-|  
|语法元素|示例|  
|在逗号 \(`,`\) 之后。|[!code-vb[VbVbalrLineContinuation#1](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_14.vb)]|  
|在左括号 \(`(`\) 之后或右括号 \(`)`\) 之前。|[!code-vb[VbVbalrLineContinuation#2](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_15.vb)]|  
|在左大括号 \(`{`\) 之后或右大括号 \(`}`\) 之前。|[!code-vb[VbVbalrLineContinuation#3](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_16.vb)]<br /><br /> 有关更多信息，请参见[对象初始值设定项：命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)或[集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)。|  
|XML 文本内嵌入式表达式的开头 \(`<%=`\) 之后或嵌入式表达式的结尾 \(`%>`\) 之前。|[!code-vb[VbVbalrLineContinuation#4](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_17.vb)]<br /><br /> 有关更多信息，请参见 [XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。|  
|在串联运算符 \(`&`\) 之后。|[!code-vb[VbVbcnConventions#9](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_18.vb)]<br /><br /> 有关更多信息，请参见[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|在赋值运算符（`=`、`&=`、`:=`、`+=`、`-=`、`*=`、`/=`、`\=`、`^=`、`<<=`、`>>=`）之后。|[!code-vb[VbVbalrLineContinuation#5](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_19.vb)]<br /><br /> 有关更多信息，请参见[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|在表达式内的二元运算符（`+`、`-`、`/`、`*`、`Mod`、`<>`、`<`、`>`、`<=`、`>=`、`^`、`>>`、`<<`、`And`、`AndAlso`、`Or`、`OrElse`、`Like`、`Xor`）之后。|[!code-vb[VbVbalrLineContinuation#7](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_20.vb)]<br /><br /> 有关更多信息，请参见[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|在 `Is` 和 `IsNot` 运算符之后。|[!code-vb[VbVbalrLineContinuation#8](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_21.vb)]<br /><br /> 有关更多信息，请参见[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|在成员限定符 \(`.`\) 之后和成员名称之前。  但是，使用 `With` 语句或在类型的初始化列表中提供值时，必须在成员限定符后面包括行继续符 \(\_\)。  在使用 `With` 语句或对象初始化列表时，请考虑在赋值运算符（例如 `=`）之后换行。|[!code-vb[VbVbalrLineContinuation#5](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_19.vb)]<br />[!code-vb[VbVbalrLineContinuation#14](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_22.vb)]<br /><br /> 有关更多信息，请参见 [With...End With 语句](../../../visual-basic/language-reference/statements/with-end-with-statement.md) 或[对象初始值设定项：命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。|  
|在 XML 轴属性限定符（`.` 或 `.@` 或 `...`）之后。  但是，在使用 `With` 关键字的情况下指定成员限定符时，必须包括行继续符 \(\_\)。|[!code-vb[VbVbalrLineContinuation#9](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_23.vb)]<br /><br /> 有关更多信息，请参见 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)。|  
|指定特性时，在小于号 \(\<\) 之后或大于号 \(`>`\) 之前。  指定特性时，还在大于号 \(`>`\) 之后。  但是，在指定程序集级别或模块级别的特性时，必须包括行继续符 \(\_\)。|[!code-vb[VbVbalrLineContinuation#10](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_24.vb)]<br /><br /> 有关更多信息，请参见 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)。|  
|在查询运算符（`Aggregate`、`Distinct`、`From`、`Group By`、`Group Join`、`Join`、`Let`、`Order By`、`Select`、`Skip`、`Skip While`、`Take`、`Take While`、`Where`、`In`、`Into`、`On`、`Ascending` 和 `Descending`）前后。  不能在由多个关键字（`Order By`、`Group Join`、`Take While` 和 `Skip While`）组成的查询运算符的关键字之间换行。|[!code-vb[VbVbalrLineContinuation#11](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_25.vb)]<br /><br /> 有关更多信息，请参见[查询](../../../visual-basic/language-reference/queries/queries.md)。|  
|在 `For Each` 语句中的 `In` 关键字之后。|[!code-vb[VbVbalrLineContinuation#12](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_26.vb)]<br /><br /> 有关更多信息，请参见 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)。|  
|在集合初始值设定项中的 `From` 关键字之后。|[!code-vb[VbVbalrLineContinuation#13](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_27.vb)]<br /><br /> 有关更多信息，请参见[集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)。|  
  
## 添加注释  
 源代码并非始终一目了然，即使对于编写它的程序员来说也是如此。  因此，为了帮助说明其代码，大部分程序员大量使用嵌入的注释。  代码中的注释可以向以后阅读或使用过程或特定指令的任何人员进行解释。  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 在编译过程中忽略注释，并且注释不影响编译后的代码。  
  
 注释行以撇号 \(`'`\) 开头或以 `REM` 开头，后跟一个空格。  注释可以添加在代码中的任意位置，但不能添加在字符串中。  若要将注释追加到某语句，请在该语句后插入一个撇号或 `REM`，后面添加注释。  注释还可以位于单独的行中。  下面的示例对这些可能情况进行了演示。  
  
 [!code-vb[VbVbalrStatements#72](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_28.vb)]  
  
## 检查编译错误  
 键入一行代码后，如果该行显示有蓝色波浪下划线（也可能显示错误信息），则该语句中有语法错误。  必须找出该语句中的错误（通过查看任务列表，或者通过将鼠标指针悬停在错误上并阅读错误信息），然后更正它。  在修复代码中的所有语法错误之前，程序无法正确地进行编译。  
  
## 相关章节  
  
|||  
|-|-|  
|术语|定义|  
|[赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)|提供指向语言参考页面（其中论述诸如 `=`、`*=` 和 `&=` 等赋值运算符）的链接。|  
|[运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)|说明如何组合元素和运算符以生成新值。|  
|[如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)|说明如何将单个语句拆分为多行以及如何将多个语句置于同一行。|  
|[如何：标记语句](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)|说明如何标记代码行。|