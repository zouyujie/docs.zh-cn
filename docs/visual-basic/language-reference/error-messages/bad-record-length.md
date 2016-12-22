---
title: "错误的记录长度 | Microsoft Docs"
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
  - "vbrID59"
dev_langs: 
  - "VB"
ms.assetid: 0926a3a4-177b-4452-9b33-d8a01e24cc21
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 错误的记录长度
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

该错误可能的原因包括：  
  
-   在 `FileGet`、`FileGetObject`、`FilePut` 或 `FilePutObject` 语句中指定的记录变量的长度与在对应的 `FileOpen` 语句中指定的长度不同。  
  
-   `FilePut` 或 `FilePutObject` 语句中的变量是变长字符串或者包括变长字符串。  
  
-   `FilePut` 或 `FilePutObject` 中的变量是 `Variant` 类型或者包括此类型。  
  
### 更正此错误  
  
1.  确保定义记录变量类型的用户定义类型中的定长变量的大小总和与 `FileOpen` 语句的 `Len` 子句中声明的值相同。  
  
2.  如果 `FilePut` 或 `FilePutObject` 语句中的变量是变长字符串或者包括变长字符串，确保变长字符串比 `FileOpen` 语句的 `Len` 子句中指定的记录长度至少少 2 个字符。  
  
3.  如果 `FilePut` 或 `FilePutObject` 中的变量是 `Variant` 类型或包括此类型，则确保变长字符串比 `FileOpen` 语句的 `Len` 子句中指定的记录长度至少少 4 个字节。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileSystem.FileGet%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.FileGetObject%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.FilePut%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.FilePutObject%2A>