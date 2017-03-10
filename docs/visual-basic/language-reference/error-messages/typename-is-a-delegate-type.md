---
title: "“&lt;类型名&gt;”是委托类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32008"
  - "vbc32008"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32008"
ms.assetid: dc6abba0-a9ad-450f-8899-87265bc84abc
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# “&lt;类型名&gt;”是委托类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

“\<typename\>”是委托类型。委托结构只允许将单个 AddressOf 表达式作为参数列表。通常可以使用 AddressOf 表达式而不使用委托结构。  
  
 创建委托类实例的 `New` 子句为委托构造函数提供了无效的参数列表。  
  
 在创建新的委托实例时，只能提供单个 `AddressOf` 表达式。  
  
 如果没有为委托构造函数传递任何参数，传递了多个参数，或者传递了不是有效 `AddressOf` 表达式的单个参数，将产生此错误。  
  
 **错误 ID：**BC32008  
  
### 更正此错误  
  
-   在 `New` 子句中，只在委托类的参数列表中使用一个 `AddressOf` 表达式。  
  
## 请参阅  
 [New 运算符](../../../visual-basic/language-reference/operators/new-operator.md)   
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [委托](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [如何：调用委托方法](../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)