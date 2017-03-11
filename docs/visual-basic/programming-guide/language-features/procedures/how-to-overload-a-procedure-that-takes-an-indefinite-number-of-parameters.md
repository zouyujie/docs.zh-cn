---
title: "如何：重载参数数量不确定的过程 (Visual Basic) | Microsoft Docs"
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
  - "过程重载, 参数数目不定"
  - "过程参数"
  - "过程, 定义"
  - "过程, 多个版本"
  - "过程, 重载"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: c7042de2-2422-4039-94e8-ac298896af69
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 如何：重载参数数量不确定的过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果过程带有 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 参数，则无法为参数数组定义带有一维数组的重载版本。  有关更多信息，请参见 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md) 中的“Implicit Overloads for a ParamArray Parameter”（ParamArray 参数的隐式重载）。  
  
### 重载带有数量可变的参数的过程  
  
1.  确定过程和调用代码逻辑受益于重载版本多于 `ParamArray` 参数。  请参见 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md) 中的“Overloads and ParamArrays”（重载和 ParamArray）。  
  
2.  确定过程应在参数列表的可变部分中接受提供的第几个值。  这可能包括无值的情况，也可能包括单个一维数组的情况。  
  
3.  为提供的值的每个可接受数量编写定义对应参数列表的 `Sub` 或 `Function` 声明语句。  请不要在此重载版本中使用 `Optional` 或 `ParamArray` 关键字。  
  
4.  在每个声明中，将 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) 关键字放在 `Sub` 或 `Function` 关键字的前面。  
  
5.  在每个声明之后，编写当调用代码提供的值对应于该声明的参数列表时应执行的过程代码。  
  
6.  根据需要，用 `End Sub` 或 `End Function` 语句终止每个过程。  
  
## 示例  
 下面的示例演示使用 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) 参数定义的过程，以及一组等效的重载过程。  
  
 [!code-vb[VbVbcnProcedures#69](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-overload-a-proced_0_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#70](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-overload-a-proced_0_2.vb)]  
  
 您不能重载这样的一个过程，其参数列表采用一维参数数组的形式。  但是，您可以使用其他隐式重载的签名。  下面的声明阐释了这一点。  
  
 [!code-vb[VbVbcnProcedures#71](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-overload-a-proced_0_3.vb)]  
  
 重载版本中的代码无需测试调用代码是否提供了一个或多个 `ParamArray` 参数值，以及提供的数量（如果提供了）。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将控制权传递给与调用参数列表匹配的版本。  
  
## 编译代码  
 因为带有 `ParamArray` 参数的过程等效于一组重载版本，所以不能重载这种带有与任何这些隐式重载对应的参数列表的过程。  有关更多信息，请参见 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)。  
  
## .NET Framework 安全性  
 每当处理可能变得无限大的数组时，都存在耗尽应用程序的某种内部容量的风险。  如果接受一个参数数组，应该测试调用代码传递给它的数组长度，如果此数组对应用程序来说太大，应采取适当的步骤。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [可选参数](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [参数数组](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [过程疑难解答](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [如何：定义一个过程的多个版本](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [如何：调用重载过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [如何：重载带有可选参数的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)