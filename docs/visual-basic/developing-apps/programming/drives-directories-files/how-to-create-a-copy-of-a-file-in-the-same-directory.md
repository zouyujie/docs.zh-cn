---
title: "如何：在同一目录中创建文件副本 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "File.Copy"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "CopyFile 方法, 使用 Visual Basic 复制文件"
  - "文件, 复制"
  - "I/O [Visual Basic], 复制文件"
  - "My.Computer.FileSystem.CopyFile 方法, 复制文件 [Visual Basic]"
ms.assetid: b2fdda86-e666-42c2-9706-9527e9fa68ff
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 如何：在同一目录中创建文件副本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 `My.Computer.FileSystem.CopyFile` 方法复制文件。  使用参数可以覆盖现有文件、重命名文件、显示操作的进度并允许用户取消操作。  
  
### 在同一文件夹中创建文件副本  
  
-   使用 `CopyFile` 方法可以提供目标文件和位置。  下面的示例创建 `test.txt` 的名为 `test2.txt` 的副本。  
  
     [!code-vb[VbVbcnMyFileSystem#51](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-create-a-copy-of-_0_1.vb)]  
  
### 通过覆盖现有文件在同一文件夹中创建文件副本  
  
-   使用 `CopyFile` 方法可以提供目标文件和位置，还可以将 `overwrite` 设置为 `True`。  下面的示例创建 `test.txt` 的名为 `test2.txt` 的副本，并用该名称覆盖任何现有文件。  
  
     [!code-vb[VbVbcnMyFileSystem#52](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-create-a-copy-of-_0_2.vb)]  
  
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
 [如何：在另一个目录中创建文件的副本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)   
 [如何：将目录复制到另一个目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-copy-a-directory-to-another-directory.md)   
 [如何：重命名文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)