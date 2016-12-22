---
title: "如何：在属性中放置值 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "属性 [Visual Basic], values"
  - "属性值"
  - "values, 属性"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 属性"
ms.assetid: c39401e5-b5fc-4439-8f31-ed640f7ce6ed
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在属性中放置值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

通过将变量名称置于赋值语句的左侧，可以在变量中存储值。  
  
 属性的 `Set` 过程存储值，但不能按名称显式调用此值。  使用属性时就像使用变量一样。  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 调用属性的过程。  
  
### 在属性中存储值  
  
1.  在赋值语句的左侧使用属性名称。  
  
     下面的示例将 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] `TimeOfDay` 属性的值设置为中午，隐式调用其 `Set` 过程。  
  
     [!CODE [VbVbcnProcedures#11](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#11)]  
  
2.  如果该属性接受参数，请在属性名后用括号将参数列表括起来。  如果无任何参数，也可以选择省略括号。  
  
3.  将参数放入括号内的参数列表中，以逗号分隔。  请确保提供变量的顺序就是属性定义相应参数的顺序。  
  
4.  将赋值语句右侧生成的值存储在属性中。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [如何：创建属性](../Topic/How%20to:%20Create%20a%20Property%20\(Visual%20Basic\).md)   
 [如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何：调用 Property 过程](../Topic/How%20to:%20Call%20a%20Property%20Procedure%20\(Visual%20Basic\).md)   
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：从属性获取值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)