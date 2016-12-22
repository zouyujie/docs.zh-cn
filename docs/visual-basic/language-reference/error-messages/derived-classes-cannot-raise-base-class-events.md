---
title: "派生类无法引发基类事件 | Microsoft Docs"
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
  - "vbc30029"
  - "bc30029"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30029"
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 派生类无法引发基类事件
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

事件只能从声明它的声明空间被引发。  因此，一个类不能引发其他任何类中的事件，即便是派生该类的类中的事件也不行。  
  
 **错误 ID：**BC30029  
  
### 更正此错误  
  
-   移动 `Event` 语句或 `RaiseEvent` 语句，使二者位于同一个类中。  
  
## 请参阅  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [RaiseEvent 语句](../../../visual-basic/language-reference/statements/raiseevent-statement.md)