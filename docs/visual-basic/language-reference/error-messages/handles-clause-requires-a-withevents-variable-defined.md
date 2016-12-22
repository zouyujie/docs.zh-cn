---
title: "Handles 子句需要在包含类型或它的基类型之一中定义的 WithEvents 变量 | Microsoft Docs"
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
  - "vbc30506"
  - "bc30506"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30506"
ms.assetid: 5b66f6a8-f050-4e03-a57f-a64e85f80cb5
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Handles 子句需要在包含类型或它的基类型之一中定义的 WithEvents 变量
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 `Handles` 子句中未提供 `WithEvents` 变量。  过程声明结尾处的 `Handles` 关键字致使其处理由使用 `WithEvents` 关键字声明的对象变量所引发的事件。  
  
 **错误 ID：**BC30506  
  
### 更正此错误  
  
-   提供必要的 `WithEvents` 变量。  
  
## 请参阅  
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)