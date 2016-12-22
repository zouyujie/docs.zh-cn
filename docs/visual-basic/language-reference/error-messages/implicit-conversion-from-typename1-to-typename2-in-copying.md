---
title: "将“ByRef”参数“&lt;参数名&gt;”的值复制回匹配参数时，发生从“&lt;类型名 1&gt;”到“&lt;类型名 2&gt;”的隐式转换。 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc41999"
  - "bc41999"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC41999"
ms.assetid: ae48c738-dff8-4c0f-8931-bbb70b2c8b03
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 将“ByRef”参数“&lt;参数名&gt;”的值复制回匹配参数时，发生从“&lt;类型名 1&gt;”到“&lt;类型名 2&gt;”的隐式转换。
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使用类型与其对应参数类型不同的 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) 变量调用了过程。  
  
 如果传递参数 `ByRef`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 有时会将参数值复制到过程中的本地变量，而不是传递引用。  在这种情况下，当过程返回时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 必须随即将局部变量值复制回调用代码中的参数。  
  
 如果将 `ByRef` 变量值复制到了过程，并且变量和参数的类型相同，则不必进行转换。  但是，如果类型不同，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 必须进行双向转换。  由于无法在过程变量或参数上使用 `CType` 或任何其他转换关键字，因此，此类转换始终是隐式的。  
  
 默认情况下，此消息是一个警告。  有关隐藏警告或将警告视为错误的信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID：**BC41999  
  
### 更正此错误  
  
-   如有可能，请使用类型与过程参数相同的调用变量，这样 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 就无需进行任何转换。  
  
-   如果需要使用与参数类型不同的变量类型来调用过程，但无需将值返回到调用变量，请将参数定义为 [ByVal](../../../visual-basic/language-reference/modifiers/byval.md)，而不是 `ByRef`。  
  
## 请参阅  
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [通过值和通过引用传递参数](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)