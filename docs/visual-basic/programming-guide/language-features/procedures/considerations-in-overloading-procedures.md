---
title: "重载过程注意事项 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], 可选"
  - "变量 [Visual Basic], 参数数组"
  - "函数重载, ParamArray 隐式重载"
  - "函数重载, 限制"
  - "函数重载, 无类型编程"
  - "Option Explicit 语句"
  - "可选参数, 重载"
  - "ParamArray 关键字, 参数和签名"
  - "ParamArray 关键字, 参数数组"
  - "ParamArray 关键字, 签名"
  - "参数数组, 重载参数"
  - "参数列表"
  - "参数, 列表"
  - "过程重载, 注意事项"
  - "过程, 重载"
  - "过程, 参数列表"
  - "限制, 重载过程"
  - "签名, ParamArray 参数"
  - "签名, 过程"
  - "无类型编程"
  - "Visual Basic 代码, 参数列表"
  - "Visual Basic 代码, 过程"
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# 重载过程注意事项 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

重载过程时，必须对每个重载版本使用不同的“签名”。  这通常意味着每个版本必须指定不同的参数列表。  有关更多信息，请参见 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md) 中的“不同签名”。  
  
 您可以在 `Sub` 过程中重载 `Function` 过程，反之亦然，只要它们有不同的签名。  如果两个重载只是一个有返回值，另一个没有，则无法进行区分。  
  
 可以按照重载过程的方式来重载属性，并且采用相同的限制。  但是，不能使用属性来重载过程，也不能使用过程来重载属性。  
  
## 可选重载版本  
 有时可能会有可选重载版本，特别是有可选参数或参数的个数可变时。  
  
 请注意，不是所有语言都支持可选参数，参数数组仅限于 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]。  如果您编写的过程可能会被多种不同语言编写的代码调用，那么重载版本提供了最大的灵活性。  
  
### 重载和可选参数  
 如果调用代码可以选择提供或省略一个或多个参数，则可以定义多个重载版本或使用可选参数。  
  
#### 何时使用重载版本  
 在以下情况可以考虑定义一系列重载版本：  
  
-   根据调用代码是否提供可选参数，过程代码中的逻辑会有显著的不同。  
  
-   过程代码无法对调用代码是否提供了可选参数进行可靠的测试。  例如，如果对于调用代码未能提供的默认值，没有可行的候选值，就是这种情况。  
  
#### 何时使用可选参数  
 在以下情况可能需要使用一个或多个可选参数：  
  
-   如果调用代码没有提供可选参数，则唯一的操作是将参数设置为默认值。  在这种情况下，如果只定义带有一个或多个 `Optional` 参数的单个版本，可以降低过程代码的复杂程度。  
  
 有关更多信息，请参见 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)。  
  
### 重载和 ParamArray  
 如果调用代码可以传递的参数个数是可变的，则可以定义多个重载版本或使用参数数组。  
  
#### 何时使用重载版本  
 在以下情况可以考虑定义一系列重载版本：  
  
-   您知道调用代码始终不会较多的值传递给参数数组。  
  
-   根据调用代码传递多少个值，过程代码中的逻辑会有显著的不同。  
  
-   调用代码可以传递不同数据类型的值。  
  
#### 何时使用参数数组  
 在以下情况更适合采用 `ParamArray` 参数：  
  
-   无法预测调用代码可以向参数数组传递多少个值，而且值的个数可能很多。  
  
-   过程逻辑对每个值执行大体相同的操作，从而可以循环访问调用代码传递的所有值。  
  
 有关更多信息，请参见 [参数数组](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)。  
  
## 可选参数的隐式重载  
 带有一个 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) 参数的过程等效于两个重载过程，其中一个过程带有这个可选参数，另一个过程不带有这个可选参数。  您不能重载这样的一个过程，其参数列表对应于这两个过程中的任何一个。  下面的声明阐释了这一点。  
  
 [!code-vb[VbVbcnProcedures#58](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/considerations-in-overlo_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#60](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/considerations-in-overlo_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#61](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/considerations-in-overlo_3.vb)]  
  
 对于带多个可选参数的过程，存在一组隐式重载，产生它们的逻辑类似于前面示例中的逻辑。  
  
## ParamArray 参数的隐式重载  
 编译器将带 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 参数的过程视为具有数量无限的重载，这些重载以调用代码传递给参数数组的内容加以区分，如下所示：  
  
-   调用代码没有向 `ParamArray` 提供参数时的一个重载  
  
-   调用代码提供了 `ParamArray` 元素类型的一维数组时的一个重载  
  
-   对于每个正整数，调用代码提供该数量的参数时的重载，每个都是 `ParamArray` 元素类型  
  
 下面的声明阐释了这些隐式重载。  
  
 [!code-vb[VbVbcnProcedures#68](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/considerations-in-overlo_4.vb)]  
  
 [!code-vb[VbVbcnProcedures#70](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/considerations-in-overlo_5.vb)]  
  
 您不能重载这样的一个过程，其参数列表采用一维参数数组的形式。  但是，您可以使用其他隐式重载的签名。  下面的声明阐释了这一点。  
  
 [!code-vb[VbVbcnProcedures#71](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/considerations-in-overlo_6.vb)]  
  
## 作为替换重载的方法 — 无类型编程  
 如果要使调用代码传递不同的数据类型与参数，一种替代方法是无类型编程。  可以使用编译器选项 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 或 [\/optionstrict](../../../../visual-basic/reference/command-line-compiler/optionstrict.md) 将类型检查开关设置为 `Off`。  这样，就不一定要声明参数的数据类型。  然而同重载相比，该方法有以下缺点：  
  
-   无类型编程产生的执行代码效率较低。  
  
-   过程必须测试每一个预期将传递的数据类型。  
  
-   如果调用代码传递了过程不支持的数据类型，编译器不能发出错误信号。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [过程疑难解答](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [如何：定义一个过程的多个版本](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [如何：调用重载过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [如何：重载带有可选参数的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何：重载参数数量不确定的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)