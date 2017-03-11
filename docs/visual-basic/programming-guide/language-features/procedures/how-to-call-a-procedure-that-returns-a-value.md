---
title: "如何：调用返回值的过程 (Visual Basic) | Microsoft Docs"
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
  - "过程调用, 返回值"
  - "过程, 调用"
  - "过程, 返回值"
  - "Visual Basic 代码, 过程"
ms.assetid: a445127b-0f5f-465a-98fb-3e514b93d115
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：调用返回值的过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`Function` 过程将值返回给调用代码。  调用该过程的方法是将其名称和参数放在赋值语句的右边或表达式中。  
  
### 在表达式中调用 Function 过程  
  
1.  使用 `Function` 过程名的方式与使用变量相同。  在表达式中可以使用变量或常数的任何位置，都可以使用 `Function` 过程调用。  
  
2.  请在过程名称后面用括号将参数列表括起来。  如果无任何参数，也可以选择省略括号。  但是，使用括号可使代码更容易阅读。  
  
3.  将参数放入括号内的参数列表中，以逗号分隔。  请确保按 `Function` 过程定义参数的顺序来提供相应的参数。  
  
     或者，可以按名称传递一个或多个参数。  有关更多信息，请参见[按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)。  
  
4.  从过程返回的值可以像变量或常数的值一样参与到表达式中。  
  
### 在赋值语句中调用 Function 过程  
  
1.  在赋值语句中的等号 \(`=`\) 后面使用 `Function` 过程。  
  
2.  请在过程名称后面用括号将参数列表括起来。  如果无任何参数，也可以选择省略括号。  但是，使用括号可使代码更容易阅读。  
  
3.  将参数放入括号内的参数列表中，以逗号分隔。  请确保按 `Function` 过程定义参数的相同顺序来提供相应的参数，除非按名称提供参数。  
  
4.  从过程返回的值存储在赋值语句左边的变量或属性中。  
  
## 示例  
 下面的示例调用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] <xref:Microsoft.VisualBasic.Interaction.Environ%2A> 来检索操作系统环境变量的值。  第一行在表达式内调用 `Environ`，第二行在赋值语句中调用它。  `Environ` 使用变量名称作为其唯一的参数，  并将变量的值返回到调用代码。  
  
 [!code-vb[VbVbcnProcedures#7](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-call-a-procedure-_0_1.vb)]  
  
## 请参阅  
 [Function 过程](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [如何：创建返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure-that-returns-a-value.md)   
 [如何：从过程返回值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-return-a-value-from-a-procedure.md)   
 [如何：调用不返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-does-not-return-a-value.md)