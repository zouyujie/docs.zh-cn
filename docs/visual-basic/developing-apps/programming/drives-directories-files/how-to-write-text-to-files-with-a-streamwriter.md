---
title: "如何：在 Visual Basic 中使用 StreamWriter 向文件中写入文本 | Microsoft Docs"
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
  - "文件, 写入"
  - "文本, 写入文件"
  - "写入文件, StreamWriter"
ms.assetid: 99762e57-ef46-4dcc-8959-a8f79c22f067
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：在 Visual Basic 中使用 StreamWriter 向文件中写入文本
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例使用 `My.Computer.FileSystem.OpenTextFileWriter` 方法打开 <xref:System.IO.StreamWriter> 对象，并使用该对象以及 <xref:System.IO.StreamWriter> 类的 <xref:System.IO.TextWriter.WriteLine%2A> 方法向文本文件中写入字符串。  
  
## 示例  
 [!code-vb[VbFileIOWrite#5](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-with-a-streamwriter_1.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   该文件已存在且是只读的 \(<xref:System.IO.IOException>\)。  
  
-   磁盘已满 \(<xref:System.IO.IOException>\)。  
  
-   路径名太长 \(<xref:System.IO.PathTooLongException>\)。  
  
## .NET Framework 安全性  
 本示例创建新的文件（如果该文件尚未存在）。  如果应用程序需要创建文件，则应用程序需要文件夹的 `Create` 访问权限。  如果该文件已经存在，则应用程序仅需要 `Write` 访问权限（一种较弱的特权）。  应尽可能在部署过程中创建文件并仅授予对单个文件的 `Read` 访问权限，而不是授予对文件夹的 `Create` 访问权限，这样做会更加安全。  
  
## 请参阅  
 <xref:System.IO.StreamWriter>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>   
 [如何：读取文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files.md)   
 [写入文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)