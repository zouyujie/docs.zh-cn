---
title: "文件编码 (Visual Basic) | Microsoft Docs"
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
  - "字符编码"
  - "文件编码"
  - "文件, 编码"
  - "Unicode, 文件编码"
ms.assetid: ea2c5f5f-bbb1-4150-9928-b9951fa6bc57
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 文件编码 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

文件编码也称为字符编码，用于指定在处理文本时如何表示字符。  一种编码可能优于另一种编码主要取决于它能处理或不能处理哪些语言字符，不过通常首选的是 Unicode。  
  
 读取或写入文件时，未正确匹配文件编码的情况可能会导致发生异常或产生不正确的结果。  
  
## 编码类型  
 处理文件时，Unicode 是首选编码。  Unicode 是全球范围的字符编码标准，该标准使用 16 位代码值来表示现代计算中使用的所有字符，包括印刷中使用的技术符号和特殊字符。  
  
 以前的字符编码标准包括传统的字符集，如使用 8 位代码值或 8 位值组合来表示特定语言或地理区域中使用的字符的 Windows ANSI 字符集。  
  
## 编码类  
 <xref:System.Text.Encoding> 类表示字符编码。  此表列出并描述了每个可用的编码类型。  
  
|||  
|-|-|  
|名称|说明|  
|<xref:System.Text.ASCIIEncoding>|表示 Unicode 字符的 ASCII 字符编码。|  
|<xref:System.Text.UnicodeEncoding>|表示 Unicode 字符的 UTF\-16 编码。|  
|<xref:System.Text.UTF32Encoding>|表示 Unicode 字符的 UTF\-32 编码。|  
|<xref:System.Text.UTF7Encoding>|表示 Unicode 字符的 UTF\-7 编码。|  
|<xref:System.Text.UTF8Encoding>|表示 Unicode 字符的 UTF\-8 编码。|  
  
## 请参阅  
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [写入文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)