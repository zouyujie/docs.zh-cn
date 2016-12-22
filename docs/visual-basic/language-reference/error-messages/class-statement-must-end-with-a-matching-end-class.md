---
title: "“Class”语句必须以匹配的“End Class”结束 | Microsoft Docs"
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
  - "vbc30481"
  - "bc30481"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30481"
ms.assetid: 583f3029-bc3a-4e06-866f-92dbecc46f19
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “Class”语句必须以匹配的“End Class”结束
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`Class` 用于开始一个 `Class` 块；因此它只能出现在块的开始，并与结束块的 `End Class` 语句成对出现。  或者存在多余的 `Class` 语句，或者没有以 `End Class` 结束 `Class` 块。  
  
 **错误 ID：**BC30481  
  
### 更正此错误  
  
-   找到并移除多余的 `Class` 语句。  
  
-   以匹配的 `End Class` 结束 `Class` 块。  
  
## 请参阅  
 [End \<关键字\> 语句](../Topic/End%20%3Ckeyword%3E%20Statement%20\(Visual%20Basic\).md)   
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)