---
title: "缺少数组下标表达式 | Microsoft Docs"
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
  - "bc30306"
  - "vbc30306"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30306"
ms.assetid: 3c0d9732-ee37-436f-a1df-29d65712f48a
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 缺少数组下标表达式
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

数组初始化遗漏了一个或多个定义数组界限的下标。  例如，语句可能包含遗漏了第三个下标的 `myArray (5,5,,10)` 表达式。  
  
 **错误 ID：**BC30306  
  
### 更正此错误  
  
-   提供丢失的下标。  
  
## 请参阅  
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)