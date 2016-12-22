---
title: "如何：在 Visual Basic 中读取固定宽度的文本文件 | Microsoft Docs"
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
  - "文件, 分析"
  - "定宽文本文件"
  - "读取文本文件, 定宽"
  - "文本文件, 读取"
  - "文本文件, 任务"
ms.assetid: 99be5692-967a-4e85-993e-cd18139a5a69
caps.latest.revision: 24
caps.handback.revision: 24
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中读取固定宽度的文本文件
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

`TextFieldParser` 对象提供了一种可以轻松而高效地分析结构化文本文件（如日志）的方法。  
  
 `TextFieldType` 属性用于定义分析文件是分隔文件还是具有固定宽度文本字段的文件。  在固定宽度的文本文件中，末尾字段的宽度可变。  若要指定末尾字段具有可变宽度，可将该字段的宽度定义为小于或等于零。  
  
### 分析固定宽度的文本文件  
  
1.  创建一个新的 `TextFieldParser`。  下面的代码创建名为 `Reader` 的 `TextFieldParser`，并打开 `test.log` 文件。  
  
     [!code-vb[VbFileIORead#9](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_1.vb)]  
  
2.  将 `TextFieldType` 属性定义为 `FixedWidth`，并定义宽度和格式。  下面的代码定义文本列；第一列的宽度为 5 个字符，第二列的宽度为 10 个字符，第三列的宽度为 11 个字符，第四列的宽度是可变的。  
  
     [!code-vb[VbFileIORead#10](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_2.vb)]  
  
3.  依次通过文件中的各个字段。  如果任何行被损坏，将报告错误并继续分析。  
  
     [!code-vb[VbFileIORead#11](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_3.vb)]  
  
4.  用 `End While` 和 `End Using` 结束 `While` 和 `Using` 块。  
  
     [!code-vb[VbFileIORead#12](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_4.vb)]  
  
## 示例  
 此示例读取文件 `test.log`。  
  
 [!code-vb[VbFileIORead#13](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-fixed-width-text-files_5.vb)]  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   无法使用指定的格式分析某行 \(<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>\)。  此异常消息指定导致发生异常的行，而 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> 属性分配给该行中包含的文本。  
  
-   指定的文件不存在 \(<xref:System.IO.FileNotFoundException>\)。  
  
-   在部分信任的情况下，用户没有访问文件的足够权限。  \(<xref:System.Security.SecurityException>\).  
  
-   路径太长 \(<xref:System.IO.PathTooLongException>\)。  
  
-   用户没有足够的权限访问文件 \(<xref:System.UnauthorizedAccessException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=fullName>   
 [如何：读取逗号分隔的文本文件](../Topic/How%20to:%20Read%20From%20Comma-Delimited%20Text%20Files%20in%20Visual%20Basic.md)   
 [如何：读取具有多种格式的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [使用 TextFieldParser 对象分析文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)   
 [演练：在 Visual Basic 中操作文件和目录](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [疑难解答：读取和写入文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [关于异常的疑难解答：Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException](../Topic/Troubleshooting%20Exceptions:%20Microsoft.VisualBasic.FileIO.TextFieldParser.MalformedLineException.md)