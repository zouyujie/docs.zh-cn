---
title: "如何：将参数传递给过程 (Visual Basic) | Microsoft Docs"
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
  - "参数传递, 过程"
  - "变量 [Visual Basic], 传递给过程"
  - "过程参数"
  - "过程参数"
  - "过程, 参数"
  - "过程, 调用"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：将参数传递给过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

调用过程时，在过程名后面加上用括号括起来的参数列表。  提供与该过程定义的每个必选参数对应的参数，而且可以根据需要为 `Optional` 参数提供参数。  如果在调用中没有提供 `Optional` 参数，则要提供任何后续参数时，必须在参数列表中加入逗号以标记该未提供参数的位置。  
  
 如果打算传递在数据类型上与对应参数的数据类型不同的参数（如 `Byte` 到 `String`），可以将类型检查开关 \([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) 设置为 `Off`。  如果 `Option Strict` 为 `On`，必须使用扩大转换或显式转换关键字。  有关更多信息，请参见 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) 和 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)。  
  
 有关更多信息，请参见 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)。  
  
### 将一个或多个参数传递到过程  
  
1.  在调用语句中，在过程名后面加上括号。  
  
2.  在括号内放入一个参数列表。  为该过程定义的每个必选参数包括一个参数，并用逗号分隔各个参数。  
  
3.  确保每个参数是有效的表达式，而且计算得出的数据类型可以转换为该过程为相应参数定义的类型。  
  
4.  如果参数定义为 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)，则可以将它加入参数列表中，也可以省略它。  如果省略它，过程会使用为该参数定义的默认值。  
  
5.  如果省略 `Optional` 参数的参数，而且在参数列表中该参数后面跟着其他参数，则可以在参数列表中加入逗号以标记已省略参数的位置。  
  
     下面的示例调用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 函数。  
  
     [!code-vb[VbVbcnProcedures#34](./codesnippet/VisualBasic/how-to-pass-arguments-to-a-procedure_1.vb)]  
  
     上面的示例提供必选的第一个参数，即要显示的消息字符串。  省略了可选的第二个参数的参数，该参数指定要在消息框上显示的按钮。  因为调用没有提供值，`MsgBox` 使用默认值 `MsgBoxStyle.OKOnly`，该值仅显示**“确定”**按钮。  
  
     参数列表中的第二个逗号标记省略的第二个参数的位置，最后一个字符串传递到 `MsgBox` 的可选的第三个参数，该参数是要在标题栏中显示的文本。  
  
## 请参阅  
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：为过程定义参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-parameter-for-a-procedure.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [递归过程](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [面向对象的编程](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)