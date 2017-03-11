---
title: "如何：在 Visual Basic 中删除文件 | Microsoft Docs"
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
  - "Delete 方法"
  - "File 对象"
  - "文件, 删除"
  - "文件, 操作"
ms.assetid: 4b721769-3e45-4be7-b7fe-b08dc4141b44
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# 如何：在 Visual Basic 中删除文件
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 `My.Computer.FileSystem` 对象的 `DeleteFile` 方法可以删除文件。  该方法提供的选项包括：是否将已删除文件发送到**“回收站”**，是否请求用户确认应删除文件，以及当用户取消该操作时执行哪些操作。  
  
### 删除文本文件  
  
-   使用 `DeleteFile` 方法删除文件。  下面的代码演示了如何删除名为 `test.txt` 的文件。  
  
     [!code-vb[VbVbcnMyFileSystem#22](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-delete-a-file_1.vb)]  
  
### 删除文本文件并请求用户确认是否应删除该文件  
  
-   使用 `DeleteFile` 方法删除该文件，并将 `showUI` 设置为 `AllDialogs`。  下面的代码演示如何删除名为 `test.txt` 的文件，以及如何允许用户确认是否应删除该文件。  
  
     [!code-vb[VbFileIOMisc#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-delete-a-file_2.vb)]  
  
### 删除文本文件并将其发送到“回收站”  
  
-   使用 `DeleteFile` 方法删除文件，并为 `recycle` 参数指定 `SendToRecycleBin`。  下面的代码演示如何删除名为 `test.txt` 的文件并发送到**“回收站”**。  
  
     [!code-vb[VbFileIOMisc#10](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-delete-a-file_3.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径（开头字符为 \\\\.  \\\) \(<xref:System.ArgumentException>\).  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路径中的文件名或文件夹名包含冒号 \(:\)，或格式无效 \(<xref:System.NotSupportedException>\)。  
  
-   该文件正在使用 \(<xref:System.IO.IOException>\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   该文件不存在 \(<xref:System.IO.FileNotFoundException>\)。  
  
-   该用户没有删除该文件的权限，或者该文件为只读 \(<xref:System.UnauthorizedAccessException>\)。  
  
-   在部分信任的情况下，用户没有足够的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   用户已取消该操作并且 `onUserCancel` 已设置为 `ThrowException` \(<xref:System.OperationCanceledException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.UICancelOption>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.UIOption>   
 <xref:Microsoft.VisualBasic.FileIO.RecycleOption>   
 [如何：获取目录中的文件集合](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)