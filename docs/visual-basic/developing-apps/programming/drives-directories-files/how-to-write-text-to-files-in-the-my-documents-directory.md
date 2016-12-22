---
title: "如何：在 Visual Basic 中将文本写入“我的文档”目录中的文件 | Microsoft Docs"
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
  - "示例 [Visual Basic], 文本文件"
  - "文件, 写入"
  - "文本, 写入文件"
  - "写入文件, 在“我的文档”中"
ms.assetid: 1c726124-781d-4976-9baa-ed46814ff3fe
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 如何：在 Visual Basic 中将文本写入“我的文档”目录中的文件
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

通过 `My.Computer.FileSystem.SpecialDirectories` 对象可以访问一些特殊目录，如**“我的文档”**目录。  
  
## 过程  
  
#### 在“我的文档”目录中写入新的文本文件  
  
1.  使用 `My.Computer.FileSystem.SpecialDirectories.MyDocuments` 属性来提供路径。  
  
     [!code-vb[VbFileIOWrite#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_1.vb)]  
  
2.  使用 `WriteAllText` 方法将文本写入指定的文件。  
  
     [!code-vb[VbVbcnMyFileSystem#14](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_2.vb)]  
  
## 示例  
 [!code-vb[VbFileIOWrite#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-text-to-files-in-the-my-documents-directory_3.vb)]  
  
## 编译代码  
 将 `test.txt` 替换为您要写入的文件的名称。  
  
## 可靠编程  
 这些代码再次引发在将文本写入文件时可能发生的所有异常。  通过使用 Windows 窗体控件（如可将用户选择项限制为有效文件名的 [OpenFileDialog](../Topic/OpenFileDialog%20Component%20\(Windows%20Forms\).md) 组件和 [SaveFileDialog](../Topic/SaveFileDialog%20Component%20\(Windows%20Forms\).md) 组件），可以减少发生异常的可能性。  但是，使用这些控件并不能杜绝出错。  在用户选择文件以及代码执行这两个时刻之间，文件系统可能会改变。  因此在处理文件时，几乎总是需要处理异常。  
  
## .NET Framework 安全性  
 如果在部分信任的上下文中运行，则代码可能会因特权不足而引发异常。  有关更多信息，请参见 [代码访问安全性基础知识](../Topic/Code%20Access%20Security%20Basics.md)。  
  
 此示例创建一个新文件。  如果应用程序需要创建文件，则该应用程序需要文件夹的“创建”权限。  权限是使用访问控制列表设置的。  如果该文件已经存在，则应用程序仅需要“写入”权限（它是一个权限较弱的特权）。  为更加安全起见，应尽可能在部署过程中创建文件，并且只授予对单个文件的“读取”特权，而不是授予文件夹的“创建”特权。  而且，更为安全的方法是将数据写入用户文件夹，而不是写入根文件夹或**“Program Files”**文件夹。  有关更多信息，请参见 [ACL Technology Overview](http://msdn.microsoft.com/zh-cn/06fbf66d-6f02-4378-b863-b2f12e349045)。  
  
## 请参阅  
 <xref:System.IO.Path.Combine%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>   
 <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>