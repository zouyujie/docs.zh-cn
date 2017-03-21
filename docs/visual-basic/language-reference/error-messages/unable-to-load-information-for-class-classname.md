---
title: "无法加载类“&lt;类名&gt;”的信息 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30712"
  - "bc30712"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30712"
ms.assetid: c7ffbd6d-05c6-4261-b44b-1bcd521bb350
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 无法加载类“&lt;类名&gt;”的信息
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

引用了不可用的类。  
  
 **错误 ID：**BC30712  
  
### 更正此错误  
  
1.  验证定义了该类并且类名称的拼写正确。  
  
2.  尝试访问该模块中声明的一个成员。  在某些情况下，因为尚未加载在其中声明成员的模块，所以调试环境不能定位成员。  
  
## 请参阅  
 [使用 Visual Studio 进行调试](/visual-studio/debugger/debugging-in-visual-studio)