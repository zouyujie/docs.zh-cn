---
title: "如何：调用 Property 过程 (Visual Basic) | Microsoft Docs"
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
  - "过程调用, 属性过程"
  - "过程, 调用"
  - "属性 [Visual Basic], 属性过程"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 属性"
ms.assetid: 96bc4d74-d9c3-4b7a-954d-58ac8553cd94
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：调用 Property 过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过将值存储在属性中或者检索属性的值，可以调用属性过程。  访问属性的方式与访问变量相同。  
  
 属性的 `Set` 过程存储一个值，而其 `Get` 过程检索该值。  但是，不可以根据名称显式调用这些过程。  您可以在赋值语句或表达式中使用该属性，就像存储或检索变量的值一样。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 调用属性的过程。  
  
### 调用属性的 Get 过程  
  
1.  在表达式中像使用变量名称一样使用属性名称。  在可以使用变量或常数的任何位置都可以使用属性。  
  
     \- 或 \-  
  
     在赋值语句中的等号 \(`=`\) 后面使用属性名称。  
  
     下面的示例读取 <xref:Microsoft.VisualBasic.DateAndTime.Now%2A> 属性值，隐式调用它的 `Get` 过程。  
  
     [!code-vb[VbVbalrDateProperties#4](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/VbVbalrDateProperties/Module1.vb#4)]  
  
2.  如果该属性接受参数，请在属性名后用括号将参数列表括起来。  如果无任何参数，也可以选择省略括号。  
  
3.  将参数放入括号内的参数列表中，以逗号分隔。  请确保提供变量的顺序就是属性定义相应参数的顺序。  
  
 属性的值像变量或常数那样参与到表达式中，或者存储在赋值语句左侧的变量或属性中。  
  
### 调用属性的 Set 过程  
  
1.  在赋值语句的左侧使用属性名称。  
  
     下面的示例通过隐式调用 `Set` 过程，设置 <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A> 属性的值。  
  
     [!code-vb[VbVbcnProcedures#11](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-call-a-property-p_2.vb)]  
  
2.  如果该属性接受参数，请在属性名后用括号将参数列表括起来。  如果无任何参数，也可以选择省略括号。  
  
3.  将参数放入括号内的参数列表中，以逗号分隔。  请确保提供变量的顺序就是属性定义相应参数的顺序。  
  
 将赋值语句右侧生成的值存储在属性中。  
  
## 请参阅  
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [如何：创建属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：在属性中放置值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)   
 [Get 语句](../../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set 语句](../../../../visual-basic/language-reference/statements/set-statement.md)