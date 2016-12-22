---
title: "如何：从过程返回值 (Visual Basic) | Microsoft Docs"
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
  - "过程, 返回值"
  - "过程, 返回自"
  - "Visual Basic 代码, 过程"
ms.assetid: 4bcc4724-2b4e-4df8-9b4b-16054607f87d
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：从过程返回值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

`Function` 过程通过执行 `Return` 语句，或在遇到 `Exit Function` 或 `End Function` 语句时，向调用代码返回一个值。  
  
### 使用 Return 语句返回值  
  
1.  在过程任务结束的地方放置一个 `Return` 语句。  
  
2.  在 `Return` 关键字后面接一个表达式，该表达式生成要返回给调用代码的值。  
  
3.  可以在同一个过程中具有多个 `Return` 语句。  
  
     下面的 `Function` 过程计算一个直角三角形的最长边（或者说斜边），并将值返回给调用代码。  
  
     [!CODE [VbVbcnProcedures#1](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#1)]  
  
     下面的示例演示了对用来存储返回值的 `hypotenuse` 的典型调用。  
  
     [!CODE [VbVbcnProcedures#6](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#6)]  
  
### 使用 Exit 函数或 End 函数返回值  
  
1.  在 `Function` 过程中的至少一个位置上为过程的名称赋值。  
  
2.  当执行 `Exit Function` 或 `End Function` 语句时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 返回赋给过程名称的最新值。  
  
3.  在同一过程中可以有多个 `Exit Function` 语句，并且在同一过程中可以混合使用 `Return` 和 `Exit Function` 语句。  
  
4.  在 `Function` 过程中只可以有一个 `End Function` 语句。  
  
     有关更多信息及示例，请参见 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md) 中的“返回值”。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub 过程](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Property 过程](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [运算符过程](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Return 语句](../../../../visual-basic/language-reference/statements/return-statement.md)   
 [如何：创建返回值的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure-that-returns-a-value.md)   
 [如何：调用返回值的过程](../Topic/How%20to:%20Call%20a%20Procedure%20That%20Returns%20a%20Value%20\(Visual%20Basic\).md)