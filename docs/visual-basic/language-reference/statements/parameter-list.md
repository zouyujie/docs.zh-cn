---
title: "参数列表 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "变量 [Visual Basic], Visual Basic"
  - "参数列表"
  - "参数, 列表"
  - "参数, Visual Basic"
  - "过程, 参数列表"
  - "Visual Basic 代码, 参数列表"
  - "Visual Basic 代码, 过程"
ms.assetid: 5d737319-0c34-4df9-a23d-188fc840becd
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 参数列表 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定调用过程时过程所需的参数 \(parameter\)。  以逗号分隔多个参数。  下面是一个参数的语法。  
  
## 语法  
  
```  
[ <attributelist> ] [ Optional ] [{ ByVal | ByRef }] [ ParamArray ]   
parametername[( )] [ As parametertype ] [ = defaultvalue ]  
```  
  
## 部件  
 `attributelist`  
 可选。  应用于此参数的特性列表。  [特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)必须用尖括号（“`<`”和“`>`”）括起来。  
  
 `Optional`  
 可选。  指定调用过程时此参数不是必选项。  
  
 `ByVal`  
 可选。  指定过程不能替换或重新分配调用代码中相应参数下的变量元素。  
  
 `ByRef`  
 可选。  指定过程可以用与调用代码本身所用的相同方式修改调用代码中的基础变量元素。  
  
 `ParamArray`  
 可选。  指定参数列表中的最后一个参数是一个可选的、数据类型为指定的数据类型的元素数组。  它允许调用代码向过程传递任意数量的参数。  
  
 `parametername`  
 必选。  表示参数的局部变量的名称。  
  
 `parametertype`  
 如果 `Option Strict` 为 `On`，则为必选项。  表示参数的局部变量的数据类型。  
  
 `defaultvalue`  
 对于 `Optional` 参数，为必选项。  任何计算为参数数据类型的常数或常数表达式。  如果类型为 `Object`，或者为类、接口、数组或结构，则默认值只能是 `Nothing`。  
  
## 备注  
 用括号将参数 \(parameter\) 括起来，并用逗号分隔各参数。  可以使用任何数据类型声明参数。  如果不指定 `parametertype`，则默认为 `Object`。  
  
 当调用代码调用过程时，它将参数 \(Argument\) 传递给每一个所需的参数 \(parameter\)。  有关更多信息，请参见 [参数和变量之间的差异](../../../visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments.md)。  
  
 调用代码传递给每个参数 \(parameter\) 的参数 \(Argument\) 为一个指针，它指向调用代码中的基础元素。  如果此元素为不可变元素（即常数、文本、枚举或表达式），则任何代码都无法更改它。  如果此元素为可变元素（即已声明的变量、字段、属性、数组元素或结构元素），则调用代码可以对其进行更改。  有关更多信息，请参见 [可修改和不可修改参数之间的差异](../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)。  
  
 如果可变元素的传入机制为 `ByRef`，则过程也可以对其进行更改。  有关更多信息，请参见 [通过值传递参数和通过引用传递参数之间的差异](../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)。  
  
## 规则  
  
-   **括号。**如果指定了参数 \(parameter\) 列表，必须将此列表置于括号内。  如果没有参数 \(parameter\)，您仍然可以用括号将空列表括起来。  这样做阐明了此元素是一个过程，从而增加了代码的可读性。  
  
-   **可选参数 \(parameter\)。**如果对某个参数使用了 `Optional` 修饰符，则列表中此参数后面的所有参数也必须为可选参数，并且必须使用 `Optional` 修饰符声明。  
  
     每个可选参数声明都必须提供 `defaultvalue` 子句。  
  
     有关更多信息，请参见 [可选参数](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)。  
  
-   **参数 \(parameter\) 数组。**必须为 `ParamArray` 参数指定 `ByVal`。  
  
     不能在同一个参数列表中同时使用 `Optional` 和 `ParamArray`。  
  
     有关更多信息，请参见 [参数数组](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)。  
  
-   **传入机制。**每个参数的默认传入机制均为 `ByVal`，这意味着过程无法更改基础变量元素。  但是，如果该元素为引用类型，则过程可以修改基础对象的内容或成员，即使它无法替换或重新分配对象本身。  
  
-   **参数 \(parameter\) 名称。**如果参数的数据类型为数组，请在 `parametername` 后紧跟括号。  有关参数 \(parameter\) 名称的更多信息，请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
## 示例  
 下面的示例演示定义两个参数 \(parameter\) 的 `Function` 过程。  
  
 [!code-vb[VbVbalrStatements#2](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/parameter-list_1.vb)]  
  
## 请参阅  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)