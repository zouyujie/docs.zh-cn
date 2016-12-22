---
title: "如何：在 Visual Basic 中创建目录 | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "目录 [Visual Basic], 创建"
  - "文件夹 [Visual Basic], 创建"
ms.assetid: 0351a2ca-24d8-43b5-bb39-9b99e6401cff
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中创建目录
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用 `My.Computer.FileSystem` 对象的 `CreateDirectory` 方法来创建目录。  
  
 如果该目录已存在，则不引发任何异常。  
  
### 创建目录  
  
-   使用 `CreateDirectory` 方法，并指定将在其中创建目录的位置的完整路径。  此示例在 `C:\Documents and Settings\All Users\Documents` 中创建目录 `NewDirectory`。  
  
     [!code-vb[VbVbcnMyFileSystem#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-create-a-directory_1.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   目录名格式不正确。  例如，它包含非法字符或仅包含空白 \(<xref:System.ArgumentException>\)。  
  
-   要创建的目录的父目录是只读的 \(<xref:System.IO.IOException>\)。  
  
-   目录名为 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   目录名太长 \(<xref:System.IO.PathTooLongException>\)。  
  
-   目录名是一个冒号“:”\(<xref:System.NotSupportedException>\)。  
  
-   用户没有创建目录的权限 \(<xref:System.UnauthorizedAccessException>\)。  
  
-   用户处于部分信任的情况，权限不足 \(<xref:System.Security.SecurityException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CreateDirectory%2A>   
 [创建、删除和移动文件和目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/creating-deleting-and-moving-files-and-directories.md)