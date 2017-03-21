---
title: "变量使用了 Visual Basic 不支持的自动化类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID458"
dev_langs: 
  - "VB"
ms.assetid: bde4f4da-493b-452c-b6e4-1d370edba4cd
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 变量使用了 Visual Basic 不支持的自动化类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试使用某个已在类型库或对象库中定义、但 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 不支持其数据类型的变量。  
  
### 更正此错误  
  
-   使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 可识别的类型的变量。  
  
     \- 或 \-  
  
-   如果在使用 `FileGet` 或 `FileGetOBject` 时遇到此错误，请确保尝试使用的文件是用 `FilePut` 或 `FilePutObject` 写入的。  
  
## 请参阅  
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)