---
title: "类不支持自动化或不支持所需的接口 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID430"
dev_langs: 
  - "VB"
ms.assetid: d985bb7e-e48e-443e-86f2-ddb86758757c
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 类不支持自动化或不支持所需的接口
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在 `GetObject` 或 `CreateObject` 函数调用中所指定的类尚未公开可编程接口，或者将项目从 .dll 更改为 .exe 或相反。  
  
### 更正此错误  
  
1.  检查创建对象的应用程序的相关文档，确定该对象类是否存在使用自动化的限制。  
  
2.  如果将项目从 .dll 更改为 .exe 或者相反，必须手动注销旧的 .dll 或 .exe。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [与我们交流](/visual-studio/ide/talk-to-us)