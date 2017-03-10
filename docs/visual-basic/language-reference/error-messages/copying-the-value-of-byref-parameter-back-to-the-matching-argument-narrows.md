---
title: "将“ByRef”参数“&lt;参数名&gt;”的值复制回匹配的参数将导致从类型“&lt;类型名 1&gt;”到类型“&lt;类型名 2&gt;”的收缩转换 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32053"
  - "vbc32053"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32053"
ms.assetid: 281564b7-99f7-451f-b10d-f985e831bb25
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 将“ByRef”参数“&lt;参数名&gt;”的值复制回匹配的参数将导致从类型“&lt;类型名 1&gt;”到类型“&lt;类型名 2&gt;”的收缩转换
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

调用过程时使用扩大到对应参数类型的变量，从参数到变量的转换则为缩小转换。  
  
 定义类或结构时，可以定义一个或多个转换运算符，将该类或结构类型转换为其他类型，  也可以定义反向转换运算符，将其他类型转换回类或结构类型。  在过程调用中使用类或结构类型时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 可以使用转换运算符将变量的类型转换为其对应参数的类型。  
  
 如果传递变量 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md)，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 有时会将变量值复制到过程的局部变量中，而是不传递引用。  在这种情况下，当过程返回时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 必须随即将局部变量值复制回调用代码中的参数。  
  
 如果将 `ByRef` 变量值复制到了过程，并且变量和参数的类型相同，则不必进行转换。  但是，如果类型不同，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 必须进行双向转换。  如果类型当中有一种是您的类或结构类型，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 就必须在该类型与其他类型之间进行双向转换。  如果这些转换当中的某一种是扩大转换，则反向转换可能会是缩小转换。  
  
 **错误 ID：**BC32053  
  
### 更正此错误  
  
-   如有可能，请使用类型与过程参数相同的调用变量，这样 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 就无需进行任何转换。  
  
-   如果需要使用与参数类型不同的变量类型来调用过程，但无需将值返回到调用变量，请将参数定义为 [ByVal](../../../visual-basic/language-reference/modifiers/byval.md)，而不是 `ByRef`。  
  
-   如果需要将值返回到调用变量中，如有可能，请将反向转换运算符定义为 [Widening](../../../visual-basic/language-reference/modifiers/widening.md)。  
  
## 请参阅  
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [通过值和通过引用传递参数](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)