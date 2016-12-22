---
title: "如何：定义一个过程的多个版本 (Visual Basic) | Microsoft Docs"
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
  - "过程重载, 多个版本"
  - "过程, 定义"
  - "过程, 多个版本"
  - "过程, 重载"
  - "Visual Basic 代码, 过程"
ms.assetid: 71ccdd66-1b00-4b66-bee4-6926c0d696f4
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：定义一个过程的多个版本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

可以通过“重载”过程将过程定义为多个版本，每个版本使用相同的名称但使用不同的参数列表。  重载的目的是定义过程的若干个密切相关的版本，而不需要通过名称来区分它们，  
  
 有关更多信息，请参见 [过程重载](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)。  
  
### 定义过程的多个版本  
  
1.  为要定义的过程的每个版本编写一个 `Sub` 或 `Function` 声明语句。  在每个声明中使用相同的过程名。  
  
2.  在每个声明中的 `Sub` 或 `Function` 关键字前面加上 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) 关键字。  可以在声明中省略 `Overloads`，但是只要有一个声明包括了此关键字，就必须在每个声明中都包括该关键字。  
  
3.  在声明语句后面编写过程代码，以处理调用代码提供的参数与该版本的参数列表匹配的情况。  无需测试调用代码提供的参数，  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会将控制权传递到过程的匹配版本。  
  
4.  根据需要，使用 `End Sub` 或 `End Function` 语句终止此过程的各个版本。  
  
## 示例  
 下面的示例定义一个 `Sub` 过程，针对客户的帐户余额发送一个事务。  它使用 `Overloads` 关键字定义此过程的两个版本，其中一个按客户姓名确定客户，另一个按帐号确定客户。  
  
 [!CODE [VbVbcnProcedures#72](../CodeSnippet/VS_Snippets_VBCSharp/VbVbcnProcedures#72)]  
  
 调用代码可以获取作为 `String` 或 `Integer` 的客户标识，然后在两种情况下使用相同的调用语句。  
  
 有关如何调用 `post` 过程的这些版本的信息，请参见 [如何：调用重载过程](../Topic/How%20to:%20Call%20an%20Overloaded%20Procedure%20\(Visual%20Basic\).md)。  
  
## 编译代码  
 请确保每个重载的版本有相同的过程名称和不同的参数列表。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [过程疑难解答](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [如何：重载带有可选参数的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何：重载参数数量不确定的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)