---
title: "如何：获取有关文件、文件夹和驱动器的信息（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "文件 [C#], 获取相关信息"
ms.assetid: 22fc2da6-5494-405b-995e-c0b99142a93e
caps.latest.revision: 30
caps.handback.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 如何：获取有关文件、文件夹和驱动器的信息（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

在 .NET Framework 中，可以使用以下类来访问文件系统信息：  
  
-   <xref:System.IO.FileInfo?displayProperty=fullName>  
  
-   <xref:System.IO.DirectoryInfo?displayProperty=fullName>  
  
-   <xref:System.IO.DriveInfo?displayProperty=fullName>  
  
-   <xref:System.IO.Directory?displayProperty=fullName>  
  
-   <xref:System.IO.File?displayProperty=fullName>  
  
 <xref:System.IO.FileInfo> 和 <xref:System.IO.DirectoryInfo> 类表示文件或目录，包含公开 NTFS 文件系统所支持的很多文件特性的属性，  同时还包含用于打开、关闭、移动和删除文件和文件夹的方法。  可以通过将表示文件、文件夹或驱动器名称的字符串传递到下面的构造函数来创建这些类的实例：  
  
```c#  
System.IO.DriveInfo di = new System.IO.DriveInfo(@"C:\");  
```  
  
 此外，还可以通过调用 <xref:System.IO.DirectoryInfo.GetDirectories%2A?displayProperty=fullName>、<xref:System.IO.DirectoryInfo.GetFiles%2A?displayProperty=fullName> 和 <xref:System.IO.DriveInfo.RootDirectory%2A?displayProperty=fullName> 来获取文件、文件夹或驱动器的名称。  
  
 <xref:System.IO.Directory?displayProperty=fullName> 和 <xref:System.IO.File?displayProperty=fullName> 类提供用于检索有关目录和文件的信息的静态方法。  
  
## 示例  
 下面的示例演示访问有关文件和文件夹的信息的各种方法。  
  
 [!CODE [csFilesandFolders#6](../CodeSnippet/VS_Snippets_VBCSharp/csFilesAndFolders#6)]  
  
## 可靠编程  
 处理用户指定的路径字符串时，还应处理在以下情况下引发的异常：  
  
-   文件名的格式不正确。  例如，包含无效字符或仅包含空白。  
  
-   文件名为空。  
  
-   文件名长于系统定义的最大长度。  
  
-   文件名包含冒号 \(:\)。  
  
 如果应用程序不具有读取指定文件所需的足够权限，则无论路径是否存在，`Exists` 方法都将返回 `false`；该方法不引发异常。  
  
## 请参阅  
 <xref:System.IO?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)