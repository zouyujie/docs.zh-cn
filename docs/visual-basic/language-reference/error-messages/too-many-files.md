---
title: "文件太多 | Microsoft Docs"
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
  - "vbrID67"
dev_langs: 
  - "VB"
ms.assetid: 2ff203e2-bba6-43ae-b72f-8e92a881c98f
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 文件太多
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

根目录下创建的文件个数超出了操作系统允许的值，或者打开的文件个数超出了 CONFIG.SYS 文件中的 **files\=** 设置。  
  
### 更正此错误  
  
1.  如果程序在根目录下打开、关闭或保存文件，则更改程序，使其使用子目录。  
  
2.  增加 CONFIG.SYS 文件中 **files\=** 设置指定的文件个数，并重新启动计算机。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)