---
title: "如何：从属性获取值 (Visual Basic) | Microsoft Docs"
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
  - "属性 [Visual Basic], values"
  - "属性值"
  - "values, 属性"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 属性"
ms.assetid: 3954423e-6ab7-4a4c-b55c-a8d27be47891
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：从属性获取值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过将属性名称包含在表达式中，可以检索属性的值。  
  
 属性的 `Get` 过程会检索该值，但并不按名称显式调用它。  使用属性时就像使用变量一样。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 调用属性的过程。  
  
### 从属性中检索值  
  
1.  在表达式中像使用变量名称一样使用属性名称。  在可以使用变量或常数的任何位置都可以使用属性。  
  
     \- 或 \-  
  
     在赋值语句中的等号 \(`=`\) 后面使用属性名称。  
  
     下面的示例读取 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] `Now` 属性值，隐式调用它的 `Get` 过程。  
  
     [!code-vb[VbVbalrDateProperties#4](./codesnippet/VisualBasic/how-to-get-a-value-from-a-property_1.vb)]  
  
2.  如果该属性接受参数，请在属性名后用括号将参数列表括起来。  如果无任何参数，也可以选择省略括号。  
  
3.  将参数放入括号内的参数列表中，以逗号分隔。  请确保提供变量的顺序就是属性定义相应参数的顺序。  
  
 属性的值像变量或常数那样参与到表达式中，或者存储在赋值语句左侧的变量或属性中。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [如何：创建属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何：调用 Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：在属性中放置值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)