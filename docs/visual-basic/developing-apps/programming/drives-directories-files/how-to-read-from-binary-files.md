---
title: "如何：在 Visual Basic 中读取二进制文件 | Microsoft Docs"
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
  - "二进制文件, 读取自"
  - "I/O [Visual Basic], 从二进制文件读取"
  - "My.Computer.FileSystem 对象, 从二进制文件读取"
  - "ReadAllBytes 方法, 从二进制文件读取"
ms.assetid: d2b1269e-24b6-42e0-9414-ae708db282d8
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：在 Visual Basic 中读取二进制文件
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`My.Computer.FileSystem` 对象提供了用于读取二进制文件的 `ReadAllBytes` 方法。  
  
### 读取二进制文件  
  
-   使用 `ReadAllBytes` 方法，以字节数组的形式返回文件的内容。  此示例读取文件 `C:/Documents and Settings/selfportrait.jpg`。  
  
     [!code-vb[VbVbcnMyFileSystem#78](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-binary-_1.vb)]  
  
-   对于大型二进制文件，可以使用 <xref:System.IO.FileStream> 对象的 <xref:System.IO.FileStream.Read%2A> 方法，一次仅从文件读取指定的量。  然后，可以限制每个读取操作将文件中的多少数据加载到内存中。  下面的代码示例复制文件，并允许调用方指定每个读取操作将文件中的多少数据读取到内存中。  
  
     [!code-vb[VbVbcnMyFileSystem#91](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-binary-_2.vb)]  
  
## 可靠编程  
 以下情况可能会导致引发异常：  
  
-   路径由于以下原因之一而无效：它是零长度字符串；它仅包含空白；它包含无效字符；或者它是一个设备路径 \(<xref:System.ArgumentException>\)。  
  
-   路径无效，因为它是 `Nothing` \(<xref:System.ArgumentNullException>\)。  
  
-   该文件不存在 \(<xref:System.IO.FileNotFoundException>\)。  
  
-   文件正由另一个进程使用，或者出现 I\/O 错误 \(<xref:System.IO.IOException>\)。  
  
-   路径超过了系统定义的最大长度 \(<xref:System.IO.PathTooLongException>\)。  
  
-   路径中的文件名或目录名包含冒号 \(:\)，或格式无效 \(<xref:System.NotSupportedException>\)。  
  
-   内存不足，无法将字符串写入缓冲区 \(<xref:System.OutOfMemoryException>\)。  
  
-   该用户缺少查看该路径所必需的权限 \(<xref:System.Security.SecurityException>\)。  
  
 不要根据文件的名称来判断文件的内容。  例如，Form1.vb 文件可能不是 Visual Basic 源文件。  
  
 在应用程序中使用输入的数据之前，需验证所有的输入内容。  文件的内容可能不是预期内容，并且用来读取该文件的方法可能失败。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>   
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [如何：读取具有多种格式的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [将数据存储到剪贴板以及从剪贴板读取数据](../../../../visual-basic/developing-apps/programming/computer-resources/storing-data-to-and-reading-from-the-clipboard.md)