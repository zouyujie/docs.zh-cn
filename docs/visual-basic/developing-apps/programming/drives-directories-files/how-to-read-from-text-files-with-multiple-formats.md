---
title: "如何：在 Visual Basic 中读取具有多种格式的文本文件 | Microsoft Docs"
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
  - "I/O [Visual Basic], 读取文本文件"
  - "My.Computer.FileSystem.WriteAllText 方法, 分析结构化文本文件"
  - "PeekChars 方法, 确定文本格式"
  - "读取文本文件, 多种格式"
  - "文本文件, 读取"
  - "TextFieldParser 对象, 从文件读取"
  - "TextFieldType 枚举"
  - "WriteAllText 方法, 分析结构化文本文件"
ms.assetid: 8d185eb2-79ca-42cd-95a7-d3ff44a5a0f8
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 如何：在 Visual Basic 中读取具有多种格式的文本文件
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.FileIO.TextFieldParser> 对象提供了一种可以轻松而高效地分析结构化文本文件（如日志）的方法。  分析整个文件时，可以通过使用 `PeekChars` 方法来确定各行的格式，从而处理具有多种格式的文件。  
  
### 分析具有多种格式的文本文件  
  
1.  将名为 testfile.txt 的文本文件添加到您的项目。  向文本文件中添加以下内容。  
  
    ```  
    Err  1001 Cannot access resource.  
    Err  2014 Resource not found.  
    Acc  10/03/2009User1      Administrator.  
    Err  0323 Warning: Invalid access attempt.  
    Acc  10/03/2009User2      Standard user.  
    Acc  10/04/2009User2      Standard user.  
    ```  
  
2.  定义预期格式以及在报告错误时使用的格式。  每个数组中的最后一项为 \-1，因此假定最后一个字段具有可变宽度。  如果数组中的最后一项小于或等于 0，则会出现这种情况。  
  
     [!code-vb[VbFileIORead#4](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_1.vb)]  
  
3.  创建一个新的 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> 对象，用于定义宽度和格式。  
  
     [!code-vb[VbFileIORead#5](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_2.vb)]  
  
4.  依次通过各行，并在读取之前测试格式。  
  
     [!code-vb[VbFileIORead#6](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_3.vb)]  
  
5.  将错误写入控制台。  
  
     [!code-vb[VbFileIORead#7](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_4.vb)]  
  
## 示例  
 下面是一个摘自 `testfile.txt` 文件的完整示例。  
  
 [!code-vb[VbFileIORead#8](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-text-files-with-multiple-formats_5.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   无法使用指定的格式分析某行 \(<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>\)。  此异常消息指定导致发生异常的行，而 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> 属性分配给该行中包含的文本。  
  
-   指定的文件不存在 \(<xref:System.IO.FileNotFoundException>\)。  
  
-   在部分信任的情况下，用户没有访问文件的足够权限。  \(<xref:System.Security.SecurityException>\).  
  
-   路径太长 \(<xref:System.IO.PathTooLongException>\)。  
  
-   用户没有足够的权限访问文件 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.PeekChars%2A>   
 <xref:Microsoft.VisualBasic.FileIO.MalformedLineException>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.EndOfData%2A>   
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.TextFieldType%2A>   
 [如何：读取逗号分隔的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [如何：读取固定宽度的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [使用 TextFieldParser 对象分析文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)