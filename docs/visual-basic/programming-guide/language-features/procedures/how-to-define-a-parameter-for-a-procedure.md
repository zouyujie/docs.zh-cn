---
title: "如何：为过程定义参数 (Visual Basic) | Microsoft Docs"
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
  - "过程参数, 定义"
  - "过程参数, 定义数据类型"
  - "过程, 定义"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 7962808d-407e-4e84-984e-43e9857c53c9
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：为过程定义参数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

“参数”允许调用代码在调用过程时将值传递到过程。  声明过程的每个参数与声明变量的方法一样，都是指定其名称和数据类型。  也可以指定传递机制，以及参数是否可选。  
  
 有关更多信息，请参见 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)。  
  
### 定义过程参数  
  
1.  在过程声明中，将参数名称添加到过程的参数列表，用逗号将它与其他参数分隔。  
  
2.  决定参数的数据类型。  
  
3.  在参数名称后加上 `As` 子句来指定数据类型。  
  
4.  决定用于参数的传递机制。  通常按值传递参数，除非希望过程能够更改其在调用代码中的值。  
  
5.  将带有 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 或 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 的参数名称放在前面，以指定传递机制。  有关更多信息，请参见 [通过值传递参数和通过引用传递参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)。  
  
6.  如果参数为可选项，将带有 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) 的传递机制放在前面，后面是带有等号 \(`=`\) 的参数数据类型以及一个默认值。  
  
     下面的示例定义一个带有三个参数的 `Sub` 过程的大纲。  前两个参数为必选，第三个参数为可选。  参数声明在参数列表中以逗号分隔。  
  
     [!code-vb[VbVbcnProcedures#33](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-define-a-paramete_1.vb)]  
  
     第一个参数接受一个 `customer` 对象，`updateCustomer` 可以直接更新传递到 `c` 的变量，因为此参数的传递方式为 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)。  过程无法更改最后两个参数的值，因为它们的传递方式为 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)。  
  
     如果调用代码不提供 `level` 参数的值，则 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 将其设置为默认值 0。  
  
     如果类型检查开关 \([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) 为 `Off`，则定义参数时 `As` 子句为可选项。  但是，如果任何一个参数使用 `As` 子句，则所有参数都使用此子句。  如果类型检查开关为 `On`，则对每个参数定义来说 `As` 子句为必选。  
  
     为所有编程元素指定数据类型称为“强类型”。  设置 `Option Strict On` 时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 强制转换为强类型。  强烈建议执行此操作，原因如下：  
  
    -   它为变量和参数启用 IntelliSense 支持。  这允许您在键入代码时看到它们的属性和其他成员。  
  
    -   允许编译器执行类型检查。  这将有助于捕捉因溢出等错误而在运行时失败的语句。  这也可以在不支持方法的对象上捕捉对方法的调用。  
  
    -   使代码的执行速度更快。  其中一个原因是如果不为编程元素指定数据类型，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器会将其分配为 `Object` 类型。  已编译的代码可能必须在 `Object` 和其他数据类型之间来回转换，这样将降低性能。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [如何：将参数传递给过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [递归过程](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [面向对象的编程](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)