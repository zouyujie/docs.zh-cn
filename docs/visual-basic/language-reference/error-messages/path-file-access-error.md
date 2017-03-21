---
title: "路径/文件访问错误 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID75"
dev_langs: 
  - "VB"
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 路径/文件访问错误
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在文件访问或磁盘访问操作期间，操作系统未能在路径和文件名之间建立连接。  
  
### 更正此错误  
  
1.  确保文件规范格式正确。  文件名可以包含完全限定（绝对）或相对路径。  完全限定路径以驱动器名称开始（如果路径在另一个驱动器上），列出从根到文件的明确路径。  任何非完全限定的路径都是相对于当前驱动器和目录的。  
  
2.  确保未尝试保存将替换现有只读文件的文件。  如果需要，请更改目标文件的只读特性，或将该文件保存为其他文件名。  
  
3.  确保未尝试以顺序的 `Output` 或 `Append` 模式打开只读文件。  如果需要，请以 `Input` 模式打开该文件或更改其只读特性。  
  
4.  确保未尝试在数据库或文档内更改 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 项目。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)