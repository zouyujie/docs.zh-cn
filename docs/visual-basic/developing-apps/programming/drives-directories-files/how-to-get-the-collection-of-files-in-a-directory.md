---
title: "如何：在 Visual Basic 中获取目录中的文件集合 | Microsoft Docs"
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
  - "文件, 访问"
  - "文件夹, 处理"
ms.assetid: 6c8ba7e8-dd37-4853-92bf-762b67c98160
caps.latest.revision: 23
caps.handback.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中获取目录中的文件集合
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=fullName> 方法的重载返回字符串的只读集合，这些字符串表示目录内文件的名称：  
  
-   将 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%28System.String%29> 重载用于指定目录中的简单文件搜索，而无需搜索子目录。  
  
-   使用 [GetFiles\(String, SearchOption, String\[\]\)](assetId:///M:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles(System.String,Microsoft.VisualBasic.FileIO.SearchOption,System.String[])?qualifyHint=False&autoUpgrade=False) 重载指定搜索的其他选项。  可以使用 `wildCards` 参数来指定搜索模式。  若要在搜索中包括子目录，请将 `searchType` 参数设置为 <xref:Microsoft.VisualBasic.FileIO.SearchOption?displayProperty=fullName>。  
  
 如果没有找到与指定模式匹配的文件，则返回一个空集合。  
  
### 列出目录中的文件  
  
-   使用其中一个 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=fullName> 方法重载，向 `directory` 参数中的搜索提供目录的名称和路径。  下面的示例返回目录中的所有文件，并将它们添加到  `ListBox1`。  
  
     [!code-vb[VbVbcnMyFileSystem#32](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-get-the-collection-of-files-in-a-directory_1.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径（开头字符为 \\\\.  \\\) \(<xref:System.ArgumentException>\).  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   `directory` 不存在 \(<xref:System.IO.DirectoryNotFoundException>\)。  
  
-   `directory` 指向某个现有文件 \(<xref:System.IO.IOException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路径中的文件名或目录名包含冒号 \(:\)，或格式无效 \(<xref:System.NotSupportedException>\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   该用户缺少必要的权限 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A>   
 [如何：查找具有特定模式的文件](../Topic/How%20to:%20Find%20Files%20with%20a%20Specific%20Pattern%20in%20Visual%20Basic.md)   
 [如何：查找具有特定模式的子目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)