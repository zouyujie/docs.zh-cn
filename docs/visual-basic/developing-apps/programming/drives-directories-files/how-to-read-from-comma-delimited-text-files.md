---
title: "如何：在 Visual Basic 中读取逗号分隔的文本文件 | Microsoft Docs"
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
  - "文件, 分析"
  - "读取文本文件, 逗号分隔的"
  - "文本文件, 读取"
  - "文本文件, 任务"
ms.assetid: a8413fe4-0dba-49c8-8692-44fb67a9ec4f
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：在 Visual Basic 中读取逗号分隔的文本文件
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

`TextFieldParser` 对象提供了一种可以轻松而高效地分析结构化文本文件（如日志）的方法。  `TextFieldType` 属性用于定义文件是符号分隔的还是具有固定宽度文本字段的。  
  
### 分析逗号分隔的文本文件  
  
1.  创建一个新的 `TextFieldParser`。  下面的代码创建名为 `MyReader` 的 `TextFieldParser`，并打开 `test.txt` 文件。  
  
     [!code-vb[VbFileIORead#15](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-comma-d_1.vb)]  
  
2.  定义 `TextField` 类型和分隔符。  下面的代码将 `TextFieldType` 属性定义为 `Delimited`，并将分隔符定义为“,”。  
  
     [!code-vb[VbFileIORead#16](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-comma-d_2.vb)]  
  
3.  依次通过文件中的各个字段。  如果遇到任何损坏的行，则报告错误，然后继续分析。  下面的代码循环访问该文件，依次显示各字段并报告所有格式不正确的字段。  
  
     [!code-vb[VbFileIORead#17](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-comma-d_3.vb)]  
  
4.  用 `End While` 和 `End Using` 结束 `While` 和 `Using` 块。  
  
     [!code-vb[VbFileIORead#18](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-comma-d_4.vb)]  
  
## 示例  
 此示例读取文件 `test.txt`。  
  
 [!code-vb[VbFileIORead#19](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-comma-d_5.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   无法使用指定的格式分析某行 \(<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>\)。  此异常消息指定导致发生异常的行，同时为 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> 属性分配该行中包含的文本。  
  
-   指定的文件不存在 \(<xref:System.IO.FileNotFoundException>\)。  
  
-   在部分信任的情况下，用户没有访问文件的足够权限。  \(<xref:System.Security.SecurityException>\).  
  
-   路径太长 \(<xref:System.IO.PathTooLongException>\)。  
  
-   用户没有足够的权限访问文件 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=fullName>   
 [如何：读取固定宽度的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [如何：读取具有多种格式的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [使用 TextFieldParser 对象分析文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)   
 [演练：在 Visual Basic 中操作文件和目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [疑难解答：读取和写入文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [关于异常的疑难解答：Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException](../Topic/Troubleshooting%20Exceptions:%20Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException.md)