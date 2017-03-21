---
title: "变量 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - " [Visual Basic], 存储"
  - "变量 [Visual Basic]"
ms.assetid: 4cfaa06d-4ae3-4307-897b-cf599dc24caa
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# 变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

在使用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 执行计算时，您通常需要存储值。  例如，可能需要计算若干值，对它们进行比较并根据比较结果执行不同的操作。  如果要比较这些值，就必须保留它们。  
  
## 用法  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 像大多数编程语言一样，使用变量来存储值。  变量具有一个名称（用于表示变量包含的值的词语）。  变量还具有数据类型（决定变量可以存储的数据类型）。  如果变量必须存储一组密切相关的索引数据项，则它可以表示数组。  
  
 局部类型推理使您能够声明变量，而无需显式声明数据类型。  而编译器将通过初始化表达式的类型推断变量的类型。  有关更多信息，请参见[局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)和 [Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)。  
  
## 赋值  
 使用赋值语句执行计算并将结果赋给变量，如下面的示例所示。  
  
 [!code-vb[VbVbalrVariables#1](../../../../visual-basic/programming-guide/language-features/variables/codesnippet/VisualBasic/index_1.vb)]  
  
> [!NOTE]
>  此示例中的等号 \(`=`\) 是赋值运算符，而不是相等运算符。  正在将值赋给变量 `applesSold`。  
  
 有关更多信息，请参见 [如何：将数据移入和移出变量](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)。  
  
## 变量和属性  
 与变量一样，属性代表您可以访问的值。  但是，它比变量更复杂。  属性使用一些代码块，这些代码块控制如何设置和检索属性的值。  有关更多信息，请参见 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)。  
  
## 请参阅  
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [变量疑难解答](../../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)   
 [如何：将数据移入和移出变量](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)   
 [Visual Basic 中属性和变量的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)