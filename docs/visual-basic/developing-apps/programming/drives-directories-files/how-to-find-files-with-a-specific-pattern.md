---
title: "如何：在 Visual Basic 中查找具有特定模式的文件 | Microsoft Docs"
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
  - "文件, 查找"
  - "模式匹配"
  - "patterns, 匹配"
ms.assetid: 25e3b71d-b844-4293-9e4e-f06c5836b5cc
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# 如何：在 Visual Basic 中查找具有特定模式的文件
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> 方法返回表示文件路径名的字符串的只读集合。  可以使用 `wildCards` 参数来指定特定模式。  如果希望在搜索中包含子目录，请将 `searchType` 参数设置为 `SearchOption.SearchAllSubDirectories`。  
  
 如果没有找到与指定模式匹配的文件，则返回一个空集合。  
  
> [!NOTE]
>  使用 `System.IO` 命名空间的 `DirectoryInfo` 选件类，有关返回文件列表的信息，请参见 <xref:System.IO.DirectoryInfo.GetFiles%2A>。  
  
### 查找具有指定模式的文件  
  
-   使用 `GetFiles` 方法，同时提供要搜索的目录的名称和路径并指定模式。  下面的示例返回目录中具有扩展名 `.dll` 的所有文件，并将它们添加到 `ListBox1` 中。  
  
     [!code-vb[VbFileIOMisc#4](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-find-files-with-a_1.vb)]  
  
## .NET Framework 安全性  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径（开头字符为 \\\\.  \\\) \(<xref:System.ArgumentException>\).  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   `directory` 不存在 \(<xref:System.IO.DirectoryNotFoundException>\)。  
  
-   `directory` 指向某个现有文件 \(<xref:System.IO.IOException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路径中的文件名或文件夹名包含冒号 \(:\)，或格式无效 \(<xref:System.NotSupportedException>\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   该用户缺少必要的权限 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>   
 [如何：查找具有特定模式的子目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)   
 [疑难解答：读取和写入文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [如何：获取目录中的文件集合](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)