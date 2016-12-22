---
title: "&lt;type1&gt;“&lt;typename&gt;”不能声明为“Overrides”，因为它不重写基 &lt;type2&gt; 中的 &lt;type1&gt; | Microsoft Docs"
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
  - "vbc30284"
  - "bc30284"
helpviewer_keywords: 
  - "BC30284"
ms.assetid: 8166bd09-dad3-495d-8cf7-66f90824a288
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;type1&gt;“&lt;typename&gt;”不能声明为“Overrides”，因为它不重写基 &lt;type2&gt; 中的 &lt;type1&gt;
当基类中不存在具有相同名称的类型时，`Sub`、`Function` 或 `Property` 语句指定 `Overrides`。  
  
 **错误 ID：**BC30284  
  
### 更正此错误  
  
1.  检查类型名称是否拼写正确。  
  
2.  删除多余的 `Overrides` 关键字。  
  
## 请参阅  
 [不在生成中：重写属性和方法](http://msdn.microsoft.com/zh-cn/2167e8f5-1225-4b13-9ebd-02591ba90213)