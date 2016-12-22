---
title: "如何：在 Visual Basic 中声明和调用默认属性 | Microsoft Docs"
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
  - "默认属性"
  - "默认属性, Visual Basic 中"
  - "默认值, 属性"
  - "过程, 定义"
  - "属性 [Visual Basic], default"
  - "Visual Basic 代码, 过程"
  - "Visual Basic 代码, 属性"
ms.assetid: 68b4026e-09ef-4613-808e-f6287494ff63
caps.latest.revision: 23
caps.handback.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中声明和调用默认属性
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

*默认属性* 是您的代码可以访问，而无需指定它的类或结构属性。  当调用命名为类或结构，但不是特性时，因此，上下文允许访问属性的访问， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 解析对该类或结构的默认属性的访问，如果存在\)。  
  
 类或结构最多只能有一个默认属性。  但是，您可以重载默认属性和具有该属性的多个版本。  
  
 有关更多信息，请参见 [Default](../../../../visual-basic/language-reference/modifiers/default.md)。  
  
### 声明默认属性  
  
1.  通常的方法声明属性。  不要指定 `Shared` 或 `Private` 关键字。  
  
2.  包括 `Default` 关键字在属性声明。  
  
3.  为属性指定至少一个参数。  您不能定义一个不带任何参数的默认属性。  
  
     [!CODE [VbVbcnProcedures#17](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#17)]  
  
### 调用默认属性  
  
1.  声明包含的类或结构类型的变量。  
  
     [!CODE [VbVbcnProcedures#16](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#16)]  
  
2.  使用单独的变量名。通常包括属性名的表达式。  
  
     [!CODE [VbVbcnProcedures#21](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#21)]  
  
3.  变量名后面加上括号将参数列表。  默认属性必须具有至少一个参数。  
  
     [!CODE [VbVbcnProcedures#20](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#20)]  
  
4.  若要检索默认属性值，请使用带有参数列表的变量名，，在表达式中或等于后 \(`=`\) 赋值语句中加上等号  
  
     [!CODE [VbVbcnProcedures#15](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#15)]  
  
5.  若要设置默认属性值，请使用变量名称，并且在赋值语句的左侧，参数列表。  
  
     [!CODE [VbVbcnProcedures#14](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#14)]  
  
6.  就象您访问其他属性，您可以使用变量名一起始终指定默认属性名称。  
  
     [!CODE [VbVbcnProcedures#19](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#19)]  
  
## 示例  
 下面的示例声明类中的默认属性。  
  
 [!CODE [VbVbcnProcedures#12](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#12)]  
  
## 示例  
 下面的示例演示如何调用类中 `class1`的默认属性 `myProperty` 。  三个赋值语句在 `myProperty`存储值，并且， <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 调用读取值。  
  
 [!CODE [VbVbcnProcedures#13](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#13)]  
  
 最常见的默认属性是在各种集合类的 <xref:Microsoft.VisualBasic.Collection.Item%2A> 属性。  
  
## 可靠编程  
 默认属性会导致源代码字符的小，减少，但是会使代码的可读性变差。  如果调用代码不熟悉您的类或结构，那么，当它引用为类或结构名称时它就不能肯定该是否引用访问类或结构，或默认属性。  这可能导致编译器错误或细小的运行时逻辑错误。  
  
 可以某些总是前面降低默认属性出错几率使用 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 将编译器类型检查为 `On`的。  
  
 如果您计划在代码中使用预定义的类或结构，则必须确定它，如果是这样，是否具有默认属性的名称。  
  
 由于这些缺点，您应该考虑不定义默认属性。  对于代码的可读性，您还应考虑始终显式引用所有属性，包括默认属性。  
  
## 请参阅  
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Default](../../../../visual-basic/language-reference/modifiers/default.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [如何：创建属性](../Topic/How%20to:%20Create%20a%20Property%20\(Visual%20Basic\).md)   
 [如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [如何：调用 Property 过程](../Topic/How%20to:%20Call%20a%20Property%20Procedure%20\(Visual%20Basic\).md)   
 [如何：在属性中放置值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [如何：从属性获取值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)