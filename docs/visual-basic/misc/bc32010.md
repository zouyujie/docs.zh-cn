---
title: "“&lt;name&gt;”不是字段或属性，因此不能命名为特性说明符中的参数。 | Microsoft Docs"
ms.custom: ""
ms.date: "10/25/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc32010"
  - "bc32010"
helpviewer_keywords: 
  - "BC32010"
ms.assetid: bfa68729-71ea-410e-bef1-83a7dab44d2a
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “&lt;name&gt;”不是字段或属性，因此不能命名为特性说明符中的参数。
特性块设置该特性的非变量成员的值。 可以仅对变量成员（如字段或属性）赋值。  
  
 **错误 ID：**BC32010  
  
### 更正此错误  
  
1.  确保特性和成员的名称拼写正确。  
  
2.  如果该成员是非变量，则从特性块中删除参数。  
  
## 请参阅  
 [不在生成中：特性的应用程序](http://msdn.microsoft.com/zh-cn/2b1703ed-4437-49b3-bc0b-568094324f47)