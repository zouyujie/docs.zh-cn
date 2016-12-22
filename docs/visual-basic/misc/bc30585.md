---
title: "无法处理事件“&lt;eventname&gt;”，因为不能从“&lt;name&gt;”访问它 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30585"
  - "vbc30585"
helpviewer_keywords: 
  - "BC30585"
ms.assetid: fe039f8f-be6f-4b52-86bd-d551c54b85cd
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 无法处理事件“&lt;eventname&gt;”，因为不能从“&lt;name&gt;”访问它
你试图处理不可访问的事件。 例如，如果 `Handles` 变量共享，则处理事件的方法也必须共享。  
  
 **错误 ID：**BC30585  
  
### 更正此错误  
  
1.  请确保该事件可访问。  
  
## 请参阅  
 [不在生成中：事件和事件处理程序](http://msdn.microsoft.com/zh-cn/95074a0d-1cbc-4221-a95a-964185c7f962)