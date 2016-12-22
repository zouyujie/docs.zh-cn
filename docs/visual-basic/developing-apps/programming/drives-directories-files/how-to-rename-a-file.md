---
title: "如何：在 Visual Basic 中重命名文件 | Microsoft Docs"
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
  - "文件, 重命名"
  - "I/O [Visual Basic], 重命名文件"
ms.assetid: 0ea7e0c8-2cb2-4bf5-a00d-7b6e3c08a3bc
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中重命名文件
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

使用 `My.Computer.FileSystem` 对象的 `RenameFile` 方法并提供当前位置、文件名和新文件名重命名文件。  此方法不能用于移动文件;使用 `MoveFile` 方法可以移动和重命名文件。  
  
### 重命名文件  
  
-   使用 `My.Computer.FileSystem.RenameFile` 方法重命名文件。  此示例文件重命名为 `Test.txt` 到 `SecondTest.txt`。  
  
     [!code-vb[VbVbcnMyFileSystem#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-rename-a-file_1.vb)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器中，此代码段位于 **文件系统 \(处理驱动器、文件夹和文件**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
## 可靠编程  
 以下情况可能会导致异常:  
  
-   路径由于以下原因之一而无效:路径是零长度字符串; 仅包含空白; 包含无效字符; 或者它设备路径 \(开头字符为 \\ \\ 中的开头  \\\) \(<xref:System.ArgumentException>\).  
  
-   `newName` 包含路径信息 \(<xref:System.ArgumentException>\)。  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   `newName` 是 `Nothing` 或为空字符串 \(<xref:System.ArgumentNullException>\)。  
  
-   源文件无效或不存在 \(<xref:System.IO.FileNotFoundException>\)。  
  
-   具有现有文件或目录与 `newName` 指定的名称 \(<xref:System.IO.IOException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路径中的文件名或目录名包含冒号 \(:\) 或格式无效 \(<xref:System.NotSupportedException>\(\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   该用户没有必需的权限 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.RenameFile%2A>   
 [如何：移动文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-move-a-file.md)   
 [创建、删除和移动文件和目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/creating-deleting-and-moving-files-and-directories.md)   
 [如何：在同一目录中创建文件副本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-the-same-directory.md)   
 [如何：在另一个目录中创建文件的副本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)