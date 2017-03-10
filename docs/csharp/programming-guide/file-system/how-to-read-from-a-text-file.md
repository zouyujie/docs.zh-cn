---
title: "如何：读取文本文件中的内容（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "StreamReader.ReadToEnd"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "读取数据, 文本文件"
  - "读取文本文件"
  - "文本文件, 读取"
  - "文本文件, 写入"
ms.assetid: 92246c5b-e819-4eea-9370-1a9460e12de3
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# 如何：读取文本文件中的内容（C# 编程指南）
此示例读取文本文件的内容以使用 <xref:System.IO.File?displayProperty=fullName> 选件类的静态方法 <xref:System.IO.File.ReadAllText%2A> 和 <xref:System.IO.File.ReadAllLines%2A>。  
  
 有关使用 <xref:System.IO.StreamReader> 的示例，请参见[如何：一次一行地读取文本文件](../../../csharp/programming-guide/file-system/how-to-read-a-text-file-one-line-at-a-time.md)。  
  
> [!NOTE]
>  本示例的文件在主题 [如何：写入文本文件](../../../csharp/programming-guide/file-system/how-to-write-to-a-text-file.md)创建。  
  
## 示例  
 [!code-cs[csFilesandFolders#4](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#4)]  
  
## 编译代码  
 将代码复制并粘贴到 C\# 控制台应用程序。  
  
 如果不使用从 [如何：写入文本文件](../../../csharp/programming-guide/file-system/how-to-write-to-a-text-file.md)的文本文件，请替换为您计算机上的参数。`ReadAllText` 和 `ReadAllLines` 使用适当的路径和文件名。  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   文件不在指定的位置存在或不存在。  检查路径和文件名的拼写。  
  
## .NET Framework 安全性  
 不要依赖文件名来确定文件的内容。  例如，文件 `myFile.cs` 可能不是 C\# 源文件。  
  
## 请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)