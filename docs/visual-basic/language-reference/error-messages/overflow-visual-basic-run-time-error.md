---
title: "溢出（Visual Basic 运行时错误） | Microsoft Docs"
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
  - "vbrERRID_Overflow"
dev_langs: 
  - "VB"
ms.assetid: c6a23279-3086-412a-bcff-ff8ed2cb8c6f
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 溢出（Visual Basic 运行时错误）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

尝试超出赋值目标限制的赋值时，会导致溢出。  
  
### 更正此错误  
  
1.  确保赋值、计算和数据类型转换的结果不会超出该变量类型所允许的取值范围，必要时，请将值赋给取值范围更大的变量类型。  
  
2.  确保属性的赋值符合属性的范围。  
  
3.  确保在计算中强制转换为整数的数值不大于整数范围。  
  
## 请参阅  
 <xref:System.Int32.MaxValue?displayProperty=fullName>   
 <xref:System.Double.MaxValue?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)