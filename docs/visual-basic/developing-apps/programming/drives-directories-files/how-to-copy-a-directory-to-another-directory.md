---
title: "如何：在 Visual Basic 中将一个目录复制到另一个目录 | Microsoft Docs"
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
  - "目录 [Visual Basic], 复制"
  - "文件夹 [Visual Basic], 复制"
  - "I/O [Visual Basic], 复制目录"
  - "I/O [Visual Basic], 复制文件夹"
ms.assetid: 2a370bd7-10ba-4219-afc4-4519d031eb6c
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：在 Visual Basic 中将一个目录复制到另一个目录
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A> 方案目录复制到另一个目录。  此方法复制目录以及目录本身。  如果目标目录不存在，则将创建。  如果同名目录于目标位置，并 `overwrite` 设置为 `False`，这两个目录的内容将合并。  可以为目录指定新名称在操作中。  
  
 在将某目录中的文件，由特定文件引发的异常可能会引发， \(如合并期间存在的文件，并且 `overwrite` 设置为 `False`时。  当引发此类异常时，它们合并为一个异常， `Data` 属性保存项文件或目录路径是键，而特定异常消息包含在相应的值。  
  
### 目录复制到另一个目录  
  
-   使用 `CopyDirectory` 方法，并指定源和目标目录的名称。  下面的示例将名为的目录复制 `TestDirectory1` 到 `TestDirectory2`，复盖现有文件。  
  
     [!code-vb[VbVbcnMyFileSystem#16](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-copy-a-directory-_1.vb)]  
  
     此代码示例也可用作 IntelliSense 代码段。  在代码段选择器，它位于 **文件系统 \(处理驱动器、文件夹和文件**。  有关更多信息，请参见 [代码段](/visual-studio/ide/code-snippets)。  
  
## 可靠编程  
 以下情况可能会导致异常:  
  
-   为目录指定的新名称包含冒号 \(:\) 或斜杠 \(\\ 或\/\) \(<xref:System.ArgumentException>\)。  
  
-   路径由于以下原因之一而无效:路径是零长度字符串; 仅包含空白; 包含无效字符; 或者它设备路径 \(开头字符为 \\ \\ 中的开头  \\\) \(<xref:System.ArgumentException>\).  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   `destinationDirectoryName` 是 `Nothing` 或为空字符串 \(<xref:System.ArgumentNullException>\)  
  
-   源目录不存在 \(<xref:System.IO.DirectoryNotFoundException>\)。  
  
-   源目录是一个根目录 \(<xref:System.IO.IOException>\)。  
  
-   组合路径指向某个现有文件 \(<xref:System.IO.IOException>\)。  
  
-   源路径和目标路径相同 \(<xref:System.IO.IOException>\)。  
  
-   `ShowUI` 设置为 `UIOption.AllDialogs` ，并且用户取消了该操作，或者目录中的一个或多个文件无法复制 \(<xref:System.OperationCanceledException>\)。  
  
-   操作循环 \(<xref:System.InvalidOperationException>\)。  
  
-   路径包含冒号 \(:\) \(<xref:System.NotSupportedException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   一个路径中的文件名或文件夹名包含冒号 \(:\) 或格式无效 \(<xref:System.NotSupportedException>\(\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   目标文件存在，但无法访问 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A>   
 [如何：查找具有特定模式的子目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)   
 [如何：获取目录中的文件集合](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)