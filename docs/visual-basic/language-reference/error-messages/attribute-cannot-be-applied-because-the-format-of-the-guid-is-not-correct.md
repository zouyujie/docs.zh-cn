---
title: "GUID“&lt;编号&gt;”的格式不正确，因此无法应用“&lt;特性&gt;” | Microsoft Docs"
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
  - "vbc32500"
  - "bc32500"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32500"
ms.assetid: 6fa34c55-368e-4d7d-b488-07a3fffe045f
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# GUID“&lt;编号&gt;”的格式不正确，因此无法应用“&lt;特性&gt;”
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`COMClassAttribute` 特性块指定的全局唯一标识符 \(GUID\) 与 GUID 的正确格式不符。  `COMClassAttribute` 使用 GUID 唯一标识类、接口以及创建事件。  
  
 一个 GUID 由 16 个字节组成，前八个字节是数字而后八个字节是二进制。  它由 Microsoft 实用工具（如 uuidgen.exe）生成并且保证在空间和时间上都是唯一的。  
  
 **错误 ID：**BC32500  
  
### 更正此错误  
  
1.  确定标识 COM 对象所需的正确 GUID。  
  
2.  确保提供给 `COMClassAttribute` 特性块的 GUID 字符串已正确复制。  
  
## 请参阅  
 <xref:System.Guid>   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)