---
title: "如何：在 Visual Basic 中在不同的目录中创建文件的副本 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "CopyFile 方法, 使用 Visual Basic 复制文件"
  - "文件, 复制"
  - "I/O [Visual Basic], 复制文件"
  - "My.Computer.FileSystem.CopyFile 方法, 复制文件 [Visual Basic]"
ms.assetid: 88e2145c-d414-45a5-ad03-6f5d58ecca26
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 如何：在 Visual Basic 中在不同的目录中创建文件的副本
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 `My.Computer.FileSystem.CopyFile` 方法可以复制文件。  该方法的参数提供了各种功能，用于覆盖现有文件、重命名文件、显示操作进度以及允许用户取消操作。  
  
### 将文本文件复制到其他文件夹  
  
-   使用 `CopyFile` 方法并指定源文件和目标目录，可以复制文件。  通过 `overwrite` 参数，可以指定是否覆盖现有文件。  下面的代码示例演示如何使用 `CopyFile`。  
  
     [!code-vb[VbFileIOMisc#24](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-create-a-copy-of-_1_1.vb)]  
  
## 可靠编程  
 以下情况可能会导致引发异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径（开头字符为 \\\\.  \\\) \(<xref:System.ArgumentException>\).  
  
-   系统未能检索绝对路径 \(<xref:System.ArgumentException>\)。  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   源文件无效或不存在 \(<xref:System.IO.FileNotFoundException>\)。  
  
-   组合路径指向某个现有目录 \(<xref:System.IO.IOException>\)。  
  
-   目标文件存在，并且 `overwrite` 设置为 `False` \(<xref:System.IO.IOException>\)。  
  
-   用户没有足够的权限访问文件 \(<xref:System.IO.IOException>\)。  
  
-   目标文件夹中的同名文件正在使用 \(<xref:System.IO.IOException>\)。  
  
-   路径中的文件名或文件夹名包含冒号 \(:\)，或格式无效 \(<xref:System.NotSupportedException>\)。  
  
-   `ShowUI` 设置为 `True`，`onUserCancel` 设置为 `ThrowException`，并且用户已取消了操作 \(<xref:System.OperationCanceledException>\)。  
  
-   `ShowUI` 设置为 `True`、`onUserCancel` 设置为 `ThrowException`，并且出现了未指定的 I\/O 错误 \(<xref:System.OperationCanceledException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   该用户没有必需的权限 \(<xref:System.UnauthorizedAccessException>\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>   
 <xref:Microsoft.VisualBasic.FileIO.UICancelOption>   
 [如何：将具有特定模式的文件复制到目录中](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-copy-files-with-a-specific-pattern-to-a-directory.md)   
 [如何：在同一目录中创建文件副本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-the-same-directory.md)   
 [如何：将目录复制到另一个目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-copy-a-directory-to-another-directory.md)   
 [如何：重命名文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)