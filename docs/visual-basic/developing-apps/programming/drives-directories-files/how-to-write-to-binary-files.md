---
title: "如何：在 Visual Basic 中写入二进制文件 | Microsoft Docs"
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
  - "二进制文件, 在 Visual Basic 中编写"
  - "文件, 二进制访问"
  - "WriteAllBytes 方法"
ms.assetid: 59fae125-de5b-4c96-883c-209f4a55112c
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：在 Visual Basic 中写入二进制文件
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A> 方法可将数据写入二进制文件。  如果 `append` 参数为 `True`，会将数据追加到文件中；否则，将覆盖文件中的数据。  
  
 如果不包括文件名的指定路径无效，将引发 <xref:System.IO.DirectoryNotFoundException> 异常。  如果此路径有效但文件不存在，将会创建该文件。  
  
### 写入二进制文件  
  
-   使用 `WriteAllBytes` 方法，并提供要写入的文件路径和名称以及字节。  此示例将数据数组 `CustomerData` 追加到名为 `CollectedData.dat` 的文件中。  
  
     [!code-vb[VbVbcnMyFileSystem#27](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-write-to-binary-f_1.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   在下列任一情况下，路径无效：路径是零长度字符串；路径仅包含空白；路径包含无效字符。  \(<xref:System.ArgumentException>\).  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   `File` 指向的路径不存在（<xref:System.IO.FileNotFoundException> 或 <xref:System.IO.DirectoryNotFoundException>）。  
  
-   文件正由另一个进程使用，或者出现 I\/O 错误 \(<xref:System.IO.IOException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路径中的文件名或目录名包含冒号 \(:\)，或格式无效 \(<xref:System.NotSupportedException>\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>   
 [如何：向文件内写入文本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-write-text-to-files.md)