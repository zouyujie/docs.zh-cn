---
title: "自动错误 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID440"
dev_langs: 
  - "VB"
ms.assetid: 2c4be5c5-2f0d-4a2b-96fe-d1b24f08fc4c
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 自动错误
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

执行方法或者获取或设置对象变量的属性时发生错误。  错误由创建该对象的应用程序报告。  
  
### 更正此错误  
  
1.  检查 `Err` 对象的属性，以确定错误来源和错误性质。  
  
2.  在紧邻访问语句之前使用 `On Error Resume Next` 语句，然后检查紧邻访问语句之后是否存在错误。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [与我们交流](/visual-studio/ide/talk-to-us)