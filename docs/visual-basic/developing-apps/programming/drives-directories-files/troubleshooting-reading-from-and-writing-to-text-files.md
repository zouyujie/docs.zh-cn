---
title: "疑难解答：读取和写入文本文件 (Visual Basic) | Microsoft Docs"
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
  - "I/O [Visual Basic], 文本文件疑难解答"
  - "读取文本文件, 疑难解答"
  - "文件 I/O 疑难解答"
  - "Visual Basic 疑难解答, 文本文件"
  - "将文本写入文件, 疑难解答"
  - "写入文件, 疑难解答"
ms.assetid: a8e9b44d-facb-4718-8c0f-466537171182
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 疑难解答：读取和写入文本文件 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本主题讨论在处理文本文件时遇到的常见问题，并为每个问题建议了一个解决方法。  
  
## 常见问题  
 在处理文本文件时所遇到的最常见问题包括安全异常、文件编码和无效路径。  
  
### 安全异常  
 在发生安全错误时，将引发 <xref:System.Security.SecurityException>。  这通常是由于用户缺少必要的权限而导致的，通过添加权限或者在独立存储中处理文件可以解决该问题。  有关更多信息，请参见[关于异常的疑难解答：System.Security.SecurityException](../Topic/Troubleshooting%20Exceptions:%20System.Security.SecurityException.md)。  
  
### 文件编码  
 文件编码也称为字符编码，用于指定在处理文本时如何表示字符。  文本文件中的意外字符可能是由于不正确的编码而导致的。  对于大多数文件，一种编码可能优于另一种编码主要取决于它能处理或不能处理哪些语言字符，不过通常首选的是 Unicode。  有关更多信息，请参见 [文件编码](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md) 和 <xref:System.Text.Encoding>。  
  
### 不正确的路径  
 在分析文件路径尤其是相对路径时，很容易提供错误的数据。  请确保提供正确的路径，这样可以纠正许多问题。  有关更多信息，请参见 [如何：分析文件路径](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [写入文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)   
 [使用 TextFieldParser 对象分析文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)