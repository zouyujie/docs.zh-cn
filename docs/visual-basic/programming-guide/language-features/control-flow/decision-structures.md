---
title: "决策结构 (Visual Basic) | Microsoft Docs"
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
  - "条件语句, 决策结构"
  - "控制流, 决策结构"
  - "决策结构"
  - "If 语句, 决策结构"
  - "If 语句, If...Then...Else"
  - "语句 [Visual Basic], 控制流"
ms.assetid: 2e2e0895-4483-442a-b17c-26aead751ec2
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# 决策结构 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中可以测试条件，然后根据该测试的结果执行不同的操作。  可以测试条件是真还是假、测试表达式的各种值，或测试执行一系列语句时所生成的各种异常。  
  
 下图显示一个决策结构，该结构测试条件是否为 true，然后根据为 true 还是 false 采取不同操作。  
  
 ![If...Then...Else 构造的流程图](../../../../visual-basic/programming-guide/language-features/control-flow/media/ifthenelse.gif "IfThenElse")  
当条件为 true 和 false 时采取不同操作  
  
## If...Then...Else 构造函数  
 使用 `If...Then...Else` 构造，可以测试一个或多个条件，然后根据各个不同条件运行一条或多条语句。  您可以通过以下方式测试条件并采取操作：  
  
-   如果条件为 `True`，则运行一个或多个语句  
  
-   如果条件为 `False`，则运行一个或多个语句  
  
-   如果条件为 `True`，则运行某些语句，如果为 `False`，则运行其他语句  
  
-   如果前一个条件为 `False`，则测试其他条件  
  
 提供所有这些可能性的控制结构是 [If...Then...Else 语句](../../../../visual-basic/language-reference/statements/if-then-else-statement.md)。  如果只有一个测试和一个语句要运行，可以使用单行版本。  如果具有一组更加复杂的条件和操作，则可以使用多行版本。  
  
## Select...Case 构造函数  
 使用 `Select...Case` 构造，可以计算一次表达式，然后根据不同的可能值运行不同的一组语句。  有关更多信息，请参见[Select...Case 语句](../../../../visual-basic/language-reference/statements/select-case-statement.md)。  
  
## Try...Catch...Finally 构造函数  
 使用 `Try...Catch...Finally` 构造，可以在这样的环境下运行一组语句：如果任何语句导致异常，该环境仍保留控制权。  您可以针对不同的异常采取不同的操作。  您还可以选择指定一个代码块，无论发生什么情况都要在退出整个 `Try...Catch...Finally` 构造前运行它。  有关更多信息，请参见[Try...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
> [!NOTE]
>  对于许多控制结构，当您单击某个关键字时，结构中的所有关键字都会突出显示。  例如，当您在 `If...Then...Else` 构造中单击 `If` 时，该构造中的所有 `If`、`Then`、`ElseIf`、`Else` 和  `End If` 实例都会突出显示。  若要移动到下一个或上一个突出显示的关键字，请按 Ctrl\+Shift\+向下键或 Ctrl\+Shift\+向上键。  
  
## 请参阅  
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [其他控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)   
 [嵌套的控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [If 运算符](../../../../visual-basic/language-reference/operators/if-operator.md)