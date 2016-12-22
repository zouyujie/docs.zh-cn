---
title: "“&lt;declaration1&gt;”无法替代“&lt;declaration2&gt;”，因为后者已声明为“NotOverridable” | Microsoft Docs"
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
  - "bc30267"
  - "vbc30267"
helpviewer_keywords: 
  - "BC30267"
ms.assetid: fb1f6797-4e49-442e-a660-59d602132631
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# “&lt;declaration1&gt;”无法替代“&lt;declaration2&gt;”，因为后者已声明为“NotOverridable”
过程或属性声明试图替代一个同名的继承元素，但该继承元素被指定为 `NotOverridable`。  
  
 **错误 ID：**BC30267  
  
### 更正此错误  
  
-   将 `NotOverridable` 关键字从继承元素的声明中删除，或删除替代声明。  
  
## 请参阅  
 [不在生成中: 替代属性和方法](http://msdn.microsoft.com/zh-cn/2167e8f5-1225-4b13-9ebd-02591ba90213)