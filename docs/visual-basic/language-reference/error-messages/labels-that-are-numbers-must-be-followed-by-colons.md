---
title: "数字标签后面必须跟冒号 | Microsoft Docs"
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
  - "vbc30801"
  - "bc30801"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30801"
ms.assetid: 67743319-2d1c-496e-bfd9-22b046b43b5a
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 数字标签后面必须跟冒号
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

行号和其他类型的标签遵守相同的规则，且必须包含冒号。  
  
 **错误 ID：**BC30801  
  
### 更正此错误  
  
-   将数字置于代码行的开始位置，并在其后加一个冒号；例如：  
  
    ```  
    400:    X += 1  
    ```  
  
## 请参阅  
 [GoTo 语句](../../../visual-basic/language-reference/statements/goto-statement.md)