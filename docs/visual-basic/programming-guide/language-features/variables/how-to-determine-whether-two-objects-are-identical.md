---
title: "如何：确定两个对象是否相同 (Visual Basic) | Microsoft Docs"
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
  - "对象变量, 确定标识"
  - "对象 [Visual Basic], 比较"
  - "测试, 对象"
ms.assetid: 7829f817-0d1f-4749-a707-de0b95e0cf5c
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：确定两个对象是否相同 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

在 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 中，如果两个变量引用的指针相同，即两个变量指向内存中的同一类实例，会认为这两个变量引用相同。  例如，在 Windows 窗体应用程序中，您可能要进行比较，确定当前实例 \(`Me`\) 与特定实例 \(`Form2`\) 是否相同。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 提供两个用来比较指针的运算符。  如果对象相同，则 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md) 返回 `True`，否则 [IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md) 返回 `True`。  
  
## 确定两个对象是否相同  
  
#### 确定两个对象是否相同  
  
1.  设置一个 `Boolean` 表达式来测试这两个对象。  
  
2.  在测试表达式中，使用 `Is` 运算符，将两个对象作为操作数。  
  
     如果两个对象指向同一类实例，则 `Is` 返回 `True`。  
  
## 确定两个对象是否不同  
 有时，您要在两个对象不同时执行操作，且不适于组合 `Not` 和 `Is`，例如 `If Not obj1 Is obj2`。  在这种情况下，可以使用 `IsNot` 运算符。  
  
#### 确定两个对象是否不同  
  
1.  设置一个 `Boolean` 表达式来测试这两个对象。  
  
2.  在测试表达式中，使用 `IsNot` 运算符，将两个对象作为操作数。  
  
     如果两个对象指向不同类实例，则 `IsNot` 返回 `True`。  
  
## 示例  
 下面的示例测试 `Object` 变量对是否指向同一类实例。  
  
 [!CODE [VbVbalrKeywords#14](../CodeSnippet/VS_Snippets_VBCSharp/VbVbalrKeywords#14)]  
  
 前面的示例显示以下输出内容。  
  
 `objA different from objB?  True`  
  
 `objA identical to objC?  True`  
  
## 请参阅  
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [如何：确定两个对象是否相关](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)