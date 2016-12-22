---
title: "如何：创建返回值的过程 (Visual Basic) | Microsoft Docs"
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
  - "过程, 定义"
  - "过程, 返回值"
  - "Visual Basic 代码, 过程"
ms.assetid: 8ee19f95-a9ef-4033-963b-d224dca207c4
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：创建返回值的过程 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用 `Function` 过程将值返回给调用代码。  
  
### 创建返回值的过程  
  
1.  在任何其他过程之外，使用一条 `Function` 语句，后跟一条 `End Function` 语句。  
  
2.  在 `Function` 语句中，`Function` 关键字后跟过程名称，随后是放在括号中的参数列表。  
  
3.  在括号后跟 `As` 子句，以指定返回值的数据类型。  
  
4.  将过程的代码语句放在 `Function` 语句与 `End Function` 语句之间。  
  
5.  使用 `Return` 语句将值返回给调用代码。  
  
     下面的 `Function` 过程通过给定的直角三角形的两条直角边计算该三角形的最长边（即斜边）。  
  
     [!CODE [VbVbcnProcedures#1](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#1)]  
  
     下面的示例演示对  `hypotenuse` 的典型调用。  
  
     [!CODE [VbVbcnProcedures#6](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#6)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [如何：从过程返回值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-return-a-value-from-a-procedure.md)   
 [如何：调用返回值的过程](../Topic/How%20to:%20Call%20a%20Procedure%20That%20Returns%20a%20Value%20\(Visual%20Basic\).md)