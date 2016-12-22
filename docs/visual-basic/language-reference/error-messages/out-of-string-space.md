---
title: "字符串空间不足 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrID14"
dev_langs: 
  - "VB"
ms.assetid: 16681c75-a400-422d-9351-c691d3c7614e
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 字符串空间不足 (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 Visual Basic 中，您可以使用非常大的字符串。  但是，其他程序的要求以及使用字符串的方法仍可能导致此错误。  
  
### 更正此错误  
  
1.  确保在计算期间需要创建临时字符串的表达式未导致此错误。  
  
2.  从内存中移除任何不必要的应用程序，以腾出更多的空间。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [字符串操作摘要](../../../visual-basic/language-reference/keywords/string-manipulation-summary.md)