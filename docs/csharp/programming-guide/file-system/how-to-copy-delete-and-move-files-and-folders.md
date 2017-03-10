---
title: "如何：复制、删除和移动文件和文件夹（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "I/O [C#]"
ms.assetid: 62e52cd7-9597-4e4a-acf9-1315f5cdbf05
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# 如何：复制、删除和移动文件和文件夹（C# 编程指南）
以下示例说明如何使用 <xref:System.IO?displayProperty=fullName> 命名空间中的 <xref:System.IO.File?displayProperty=fullName>、<xref:System.IO.Directory?displayProperty=fullName>、<xref:System.IO.FileInfo?displayProperty=fullName> 和 <xref:System.IO.DirectoryInfo?displayProperty=fullName> 类以同步方式复制、移动和删除文件和文件夹。  这些示例没有提供进度栏或其他任何用户界面。  如果您想提供一个标准进度对话框，请参见[如何：提供文件操作进度对话框](../../../csharp/programming-guide/file-system/how-to-provide-a-progress-dialog-box-for-file-operations.md)。  
  
 在操作多个文件时，请使用 <xref:System.IO.FileSystemWatcher?displayProperty=fullName> 提供一些事件，以便可以利用这些事件计算进度。  另一种方法是使用平台调用来调用 Windows Shell 中相应的文件相关方法。  有关如何异步执行这些文件操作的信息，请参见[异步文件 I\/O](../Topic/Asynchronous%20File%20I-O.md)。  
  
## 示例  
 下面的示例演示如何复制文件和目录。  
  
 [!code-cs[csFilesandFolders#7](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#7)]  
  
## 示例  
 下面的示例演示如何移动文件和目录。  
  
 [!code-cs[csFilesandFolders#8](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#8)]  
  
## 示例  
 下面的示例演示如何删除文件和目录。  
  
 [!code-cs[csFilesandFolders#9](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#9)]  
  
## 请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)   
 [如何：提供文件操作进度对话框](../../../csharp/programming-guide/file-system/how-to-provide-a-progress-dialog-box-for-file-operations.md)   
 [文件和流 I\/O](../Topic/File%20and%20Stream%20I-O.md)   
 [通用 I\/O 任务](../Topic/Common%20I-O%20Tasks.md)