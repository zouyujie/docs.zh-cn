---
title: "不带必需参数的属性不能声明为“Default” | Microsoft Docs"
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
  - "vbc31048"
  - "bc31048"
helpviewer_keywords: 
  - "BC31048"
ms.assetid: 27ef4bc9-532f-4097-a7fc-a645fd5387a3
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 不带必需参数的属性不能声明为“Default”
指定属性不带必需参数，但带有 `Default` 修饰符。  
  
 **错误 ID：**BC31048  
  
### 更正此错误  
  
-   声明默认属性的必需参数。  
  
-   从属性定义中删除 `Default` 修饰符。  
  
## 请参阅  
 [不在生成中：默认属性](http://msdn.microsoft.com/zh-cn/a70f2a27-8176-4858-935e-f25afdd43ab5)