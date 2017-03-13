---
title: "如何：在 Visual Basic 中向文件内写入文本 | Microsoft Docs"
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
  - "示例 [Visual Basic], 文本文件"
  - "文件, 写入"
  - "文本, 写入文件"
  - "写入文件"
ms.assetid: 304956eb-530d-4df7-b48f-9b4d1f2581a0
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：在 Visual Basic 中向文件内写入文本
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> 方法可以用于向文件中写入文本。  如果指定的文件不存在，则创建该文件。  
  
## 过程  
  
#### 向文件中写入文本  
  
-   使用 `WriteAllText` 方法向文件中写入文本，同时指定要写入的文件和文本。  此示例向名为 `test.txt` 的文件中写入 `"This is new text."` 这一行，并将这行文本追加到此文件中现有的任何文本之后。  
  
     [!code-vb[VbFileIOWrite#3](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files_1.vb)]  
  
#### 向文件中写入一系列字符串  
  
-   循环通过字符串集合。  使用 `WriteAllText` 方法向文件中写入文本，同时指定目标文件以及要添加的字符串，并将 `append` 设置为 `True`。  
  
     此示例将 `Documents and Settings` 目录中文件的名称写入 `FileList.txt` 中，同时在每个名称之间插入一个回车符以获得更好的可读性。  
  
     [!code-vb[VbFileIOWrite#4](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files_2.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径（开头字符为 \\\\.  \\\) \(<xref:System.ArgumentException>\).  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   `File` 指向的路径不存在（<xref:System.IO.FileNotFoundException> 或 <xref:System.IO.DirectoryNotFoundException>）。  
  
-   文件正由另一个进程使用，或者出现 I\/O 错误 \(<xref:System.IO.IOException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路径中的文件名或目录名包含冒号 \(:\)，或格式无效 \(<xref:System.NotSupportedException>\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
-   磁盘已满，并且对 `WriteAllText` 的调用失败 \(<xref:System.IO.IOException>\)。  
  
 如果在部分信任的上下文中运行，则代码可能会因特权不足而引发异常。  有关更多信息，请参见 [代码访问安全性基础知识](../Topic/Code%20Access%20Security%20Basics.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>   
 [如何：读取文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files.md)