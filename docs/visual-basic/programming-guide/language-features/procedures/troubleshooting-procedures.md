---
title: "过程疑难解答 (Visual Basic) | Microsoft Docs"
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
  - "过程, 关于过程"
  - "过程, 疑难解答"
  - "过程疑难解答"
  - "Visual Basic 疑难解答, 过程"
  - "Visual Basic 代码, 过程"
ms.assetid: 525721e8-2e02-4f75-b5d8-6b893462cf2b
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 过程疑难解答 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本页列出在使用过程时可能遇到的一些常见问题。  
  
## 从 Function 过程返回数组类型  
 如果 `Function` 过程返回某个数组的数据类型，您就不能使用 `Function` 名称将值存储在该数组的元素中。  如果尝试这样做，编译器会将它解释为对 `Function` 的调用。  下面的示例将产生编译器错误：  
  
 `Function allOnes(ByVal n As Integer) As Integer()`  
  
 `For i As Integer = 1 To n - 1`  
  
 `' The following statement generates a`   `COMPILER ERROR`  `.`  
  
 `allOnes(i) = 1`  
  
 `Next i`  
  
 `' The following statement generates a`   `COMPILER ERROR`  `.`  
  
 `Return allOnes()`  
  
 `End Function`  
  
 语句 `allOnes(i) = 1` 将生成编译器错误，因为它看起来使用了数据类型不正确（单个 `Integer` 而不是 `Integer` 数组）的参数来调用 `allOnes`。  语句 `Return allOnes()` 也将生成编译器错误，因为它看起来在调用 `allOnes` 时未使用参数。  
  
 **纠正措施：**若要能够修改即将返回的数组的元素，请将内部数组定义为局部变量。  下面的示例在编译时没有错误。  
  
 [!code-vb[VbVbcnProcedures#66](./codesnippet/VisualBasic/troubleshooting-procedures_1.vb)]  
  
## 参数不能被过程调用修改  
 如果打算在调用代码中允许过程更改某个参数下的编程元素，您必须通过引用来传递该元素。  但是即使您通过值传递该元素，过程仍可访问引用类型参数的元素。  
  
-   **基础变量**。  若要允许过程替换基础变量元素本身的值，该过程必须声明参数 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)。  此外，不允许调用代码将参数置于括号内，因为这样做将重写 `ByRef` 传入机制。  
  
-   **引用类型元素** 如果声明了参数 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)，则过程不能修改基础变量元素本身。  但是，如果参数为引用类型，则过程可以修改它指向的对象成员，即使它无法替换变量的值。  例如，如果参数为数组变量，则过程不能向它分配新的数组，但可以更改它的一个或多个元素。  更改的元素在调用代码中的基础数组变量中反映出来。  
  
 下面的示例定义两个过程，它们按值获得数组变量并对其元素进行操作。  过程 `increase` 只是给每个元素加上 1。  过程 `replace` 向参数 `a()` 分配一个新数组，然后给每个元素加上 1。  但是，重新分配并不会影响调用代码中的基础数组变量，因为 `a()` 被声明为 `ByVal`。  
  
 [!code-vb[VbVbcnProcedures#35](./codesnippet/VisualBasic/troubleshooting-procedures_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#38](./codesnippet/VisualBasic/troubleshooting-procedures_3.vb)]  
  
 下面的示例调用 `increase` 和 `replace`。  
  
 [!code-vb[VbVbcnProcedures#37](./codesnippet/VisualBasic/troubleshooting-procedures_4.vb)]  
  
 第一个 `MsgBox` 调用显示“After increase\(n\): 11, 21, 31, 41”。  由于 `n` 是引用类型，因此 `increase` 可以更改它的成员（即使它的传递机制为 `ByVal`）。  
  
 第二个 `MsgBox` 调用显示“After replace\(n\): 11, 21, 31, 41”。  由于 `n` 的传递机制为 `ByVal`，因此 `replace` 不能通过向变量 `n` 分配新数组来对其进行修改。  当 `replace` 创建新的数组实例 `k`，并将其赋给局部变量 `a` 时，它将丢失由调用代码传入的对 `n` 的引用。  当它递增 `a` 的成员时，只有局部数组 `k` 受影响。  
  
 **纠正措施：**若想能够修改基础变量元素本身，请通过引用传递它。  下面的示例演示 `replace` 声明中的更改，此更改允许它在调用代码中将一个数组替换为另一个数组。  
  
 [!code-vb[VbVbcnProcedures#64](./codesnippet/VisualBasic/troubleshooting-procedures_5.vb)]  
  
## 无法定义重载  
 如果要定义过程的重载版本，必须使用相同的名称和不同的签名。  如果编译器无法将声明与具有相同签名的重载区分开来，它就会生成一条错误。  
  
 过程的“签名”由过程名称和参数列表确定。  每个重载的名称必须与其他所有重载的名称相同，但至少有一个签名组件必须与其他所有重载的签名组件不同。  有关更多信息，请参见 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)。  
  
 下面的项即使与参数列表相关，也不是过程签名的组件：  
  
-   过程修饰符关键字，如 `Public`、`Shared` 和 `Static`  
  
-   参数名称  
  
-   参数修饰符关键字，如 `ByRef` 和 `Optional`  
  
-   返回值的数据类型（转换运算符除外）  
  
 您不能通过只改变一个或多个前面的项来重载过程。  
  
 **纠正措施：**若想能够定义过程重载，必须改变签名。  由于必须使用相同的名称，因此必须改变参数的编号、顺序或数据类型。  在泛型过程中，可以改变类型参数的编号。  在转换运算符 \([CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)\) 中，可以改变返回类型。  
  
### 使用 Optional 和 ParamArray 参数重载决策  
 如果要使用一个或多个 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) 参数或一个 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 参数重载过程，则必须避免复制任何“隐式重载”。  有关信息，请参见 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)。  
  
## 调用错误的重载过程版本  
 如果过程具有多个重载版本，您必须熟悉这些版本的所有参数列表并了解 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 如何在重载之间解析调用。  否则，您调用的重载可能并不是您所需的重载。  
  
 确定要调用哪个重载时，请注意要遵循以下规则：  
  
-   提供正确的参数编号，并且参数顺序正确无误。  
  
-   理想情况下，参数 \(Argument\) 的数据类型应与相应参数 \(parameter\) 的数据类型完全相同。  无论如何，每个参数 \(Argument\) 的数据类型都必须扩大为其相应参数 \(parameter\) 的数据类型。  即使在 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 设置为 `Off` 的情况下，也是如此。  如果某个重载需要根据参数列表进行任何收缩转换，就不能调用该重载。  
  
-   如果提供的参数 \(Argument\) 需要扩大，请使它们的数据类型尽可能接近相应参数 \(Parameter\) 的数据类型。  如果同时有两个或多个重载接受您的参数 \(Argument\) 数据类型，编译器将解析您对那个需要最少扩大量的重载的调用。  
  
 准备参数时，可以通过使用 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md) 转换关键字来减少数据类型不匹配的机会。  
  
### 重载决策失败  
 调用重载过程时，编译器尝试消除除某个重载之外的所有重载。  如果消除成功，编译器将解析对该重载的调用。  如果编译器消除了所有重载或者无法将合格的重载减少为单个候选重载，则会生成一条错误。  
  
 下面的示例阐释了此重载决策过程。  
  
 [!code-vb[VbVbcnProcedures#62](./codesnippet/VisualBasic/troubleshooting-procedures_6.vb)]  
  
 [!code-vb[VbVbcnProcedures#63](./codesnippet/VisualBasic/troubleshooting-procedures_7.vb)]  
  
 在第一个调用中，编译器将消除第一个重载，因为第一个参数 \(Argument\) 的类型 \(`Short`\) 将收缩为相应参数 \(Parameter\) 的类型 \(`Byte`\)。  接着，编译器消除第三个重载，因为第二个重载中的每个参数 \(Argument\) 类型（`Short` 和 `Single`）都将扩大为第三个重载中的相应类型（`Integer` 和 `Single`）。  第二个重载需要的扩大量较少，因此编译器将用它进行调用。  
  
 在第二个调用中，编译器不能根据收缩消除任何重载。  与第一个调用中的原因相同，编译器将消除第三个重载，因为它可以用参数 \(Argument\) 类型的最少扩大量调用第二个重载。  然而，编译器无法在第一个和第二个重载之间解析。  每个重载都有一个已定义的参数类型，该类型将扩大到另一个重载中的相应类型（从 `Byte` 扩大为 `Short`，但从 `Single` 扩大为 `Double`）。  编译器因此生成重载决策错误。  
  
 **纠正措施：**若想在调用重载过程时不出现多义性，请使用 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md) 将参数 \(Argument\) 数据类型与参数 \(parameter\) 类型匹配。  下面的示例演示对强制解析第二个重载的 `z` 的调用。  
  
 [!code-vb[VbVbcnProcedures#65](./codesnippet/VisualBasic/troubleshooting-procedures_8.vb)]  
  
### 使用 Optional 和 ParamArray 参数重载决策  
 如果过程的两个重载具有相同的签名，但在其中一个重载中将最后一个参数声明为 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)，而在另一个重载中将最后一个参数声明为 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)，则编译器将根据最匹配原则解析最匹配的那个过程的调用。  有关更多信息，请参见 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)