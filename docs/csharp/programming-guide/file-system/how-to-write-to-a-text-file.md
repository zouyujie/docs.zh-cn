---
title: "如何：写入文本文件（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "TextWriter.WriteLine"
  - "StreamWriter.Close"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "文件 [C#], 文本文件"
  - "文本, 写入文件 [C#]"
ms.assetid: 2e99f184-d88b-4719-a7f1-d9ec482aa809
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# 如何：写入文本文件（C# 编程指南）
以下示例给出了将文本写入文件的各种方法。  前两个示例对 <xref:System.IO.File?displayProperty=fullName> 类使用静态便捷方法以将任何 IEnumerable\<string\> 的每个元素和一个字符串写入文本文件。  示例 3 展示了在写入文件时必须分别处理文本的每一行时，如何将文本添加到文件。  示例 1\-3 覆盖文件中的所有现有内容，但示例 4 展示如何将文本追加到现有文件。  
  
 这些示例均会将字符串文本写入文件，但是你更有可能需要使用 <xref:System.String.Format%2A> 方法，此方法具有很多用于写入不同类型值的控件，包括在字段中左右对齐、有无边距等。  还可以使用 C\# [字符串内插](../../../csharp/language-reference/keywords/interpolated-strings.md)功能。  
  
## 示例  
 [!code-cs[csFilesandFolders#3](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-write-to-a-text-file_1.cs)]  
  
 这些示例均会将字符串文本写入文件，但是你更有可能需要使用 <xref:System.String.Format%2A> 方法，此方法具有很多用于写入不同类型值的控件，包括在字段中左右对齐、有无边距等。  还可以使用 C\# [字符串内插](../../../csharp/language-reference/keywords/interpolated-strings.md)功能。  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   文件已存在并且为只读。  
  
-   路径名可能太长。  
  
-   磁盘可能已满。  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)   
 [示例：将集合保存到应用程序存储](http://code.msdn.microsoft.com/CSWinStoreAppSaveCollection-bed5d6e6)