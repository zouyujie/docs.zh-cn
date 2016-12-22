---
title: "错误的文件名或文件号 | Microsoft Docs"
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
  - "vbrID52"
dev_langs: 
  - "VB"
ms.assetid: d0e96aea-7621-48f6-a78b-5d37d18aaa4e
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 错误的文件名或文件号
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

尝试访问指定文件时发生错误。  该错误可能的原因包括：  
  
-   某个语句所引用的文件的文件名或编号未在 `FileOpen` 语句中指定，或在 `FileOpen` 语句中指定，但随后被关闭。  
  
-   某个语句所引用的文件的编号超出了文件编号范围。  
  
-   某个语句所引用的文件的文件名或编号无效。  
  
### 更正此错误  
  
1.  确保在 `FileOpen` 语句中指定了该文件名。  请注意，如果调用 `FileClose` 语句时不使用参数，可能会意外地关闭所有打开的文件。  
  
2.  如果代码以算法形式生成文件编号，则确保编号有效。  
  
3.  检查文件名，确保它们符合操作系统约定。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>   
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)