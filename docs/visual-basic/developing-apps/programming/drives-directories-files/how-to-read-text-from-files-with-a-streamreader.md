---
title: "如何：使用 StreamReader 读取文件中的文本 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "文件, 读取"
  - "读取文件, 文本"
  - "从文件中读取文本"
  - "文本, 从文件读取"
ms.assetid: 384033c6-18f9-4d59-9610-36371226558f
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：使用 StreamReader 读取文件中的文本 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

`My.Computer.FileSystem` 对象提供打开 <xref:System.IO.TextReader> 和 <xref:System.IO.TextWriter> 的方法。  这些方法（`OpenTextFileWriter` 和 `OpenTextFileReader`）为高级方法，除非您选择**“全部”**选项卡，否则它们不会显示在 IntelliSense 中。  
  
### 使用文本读取器读取文件中的行  
  
-   使用 `OpenTextFileReader` 方法打开 <xref:System.IO.TextReader>，同时指定文件。  此示例打开名为 `testfile.txt` 的文件，读取其中的一行并将该行显示在消息框中。  
  
     [!code-vb[VbFileIORead#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-text-from-files-with-a-streamreader_1.vb)]  
  
## 可靠编程  
 读取的文件必须为文本文件。  
  
 不要根据文件的名称来判断文件的内容。  例如，Form1.vb 文件可能不是 Visual Basic 源文件。  
  
 在应用程序中使用输入的数据之前，需验证所有的输入内容。  文件的内容可能不是预期内容，并且用来读取该文件的方法可能失败。  
  
## .NET Framework 安全性  
 若要读取文件，程序集需要由 <xref:System.Security.Permissions.FileIOPermission> 类授予的特权级别。  如果在部分信任的上下文中运行，则代码可能会因特权不足而引发异常。  有关更多信息，请参见 [代码访问安全性基础知识](../Topic/Code%20Access%20Security%20Basics.md)。  用户还需要该文件的访问权限。  有关更多信息，请参见 [ACL Technology Overview](http://msdn.microsoft.com/zh-cn/06fbf66d-6f02-4378-b863-b2f12e349045)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:System.Windows.Forms.OpenFileDialog>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A>   
 [SaveFileDialog 组件](../Topic/SaveFileDialog%20Component%20\(Windows%20Forms\).md)   
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)